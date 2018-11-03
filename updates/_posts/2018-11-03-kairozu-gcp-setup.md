---
layout: content
title: Django Project on GCP
tags: project
---
This is a quick step-by-step for moving your Django project onto a Google Cloud Platform f1-micro instance (which falls into the free tier). It assumes you already have a Google Cloud Platform account, that you're syncing your Django project with a GitHub repository, and that you're using a PostgreSQL database with your Django project.

1. Create the f1-micro instance on Google Cloud Platform.
2. Update system and install software.
3. Configure GitHub access, clone your repository, and run Django migrations.
4. Configure Gunicorn, the NGINX web server, and Supervisor.
5. Install, set up, and configure Certbot.
6. Import previous data, perform other odds & ends, and run the server!

## Create f1-micro Instance on Google Cloud Platform
Create an account to use the <a href="https://console.cloud.google.com">Google Cloud Console</a>. Once you've logged in and created a project, in the Navigation Menu, click through "Compute Engine", "VM Instances", and then "Create Instance" at the top of the screen. Choose a name, a region, and a zone, and then under "Machine Type" select "micro (1 shared vCPU)" -- leave the other options as default. Under "Firewall" select both "Allow HTTP traffic" and "Allow HTTPS traffic" and then click "Create" at the bottom of the page.

You can connect via SSH through the <a href="https://console.cloud.google.com/compute/instances">VM Instances</a> page -- click "SSH" in the row of your instance, and a console window should pop up and connect to your instance.

## Update System & Install Software
Run the following commands to update system software, install necessary software, and if desired, create swap space. Replace 'projectname' with you desired project name, and 'username' and 'groupname' with your user and group names (generally the same in this case) respectively. The things that you install with <code>pip install</code> will depend on your project, of course.

```terminal
$ sudo apt-get update
$ sudo apt-get dist-upgrade
$ sudo apt-get install postgresql git unzip nginx virutalenv supervisor

$ sudo virtualenv -p python3 /opt/projectname
$ sudo chown -R username:groupname /opt/projectname
$ source /opt/projectname/bin/activate

(projectname) $ pip install django
(projectname) $ pip install djangorestframework
(projectname) $ pip install django-nested-admin
(projectname) $ pip install django-model-utils
(projectname) $ pip install django-extensions
(projectname) $ pip install gunicorn
(projectname) $ pip install psycopg2-binary
(projectname) $ deactivate

$ sudo fallocate -l 2G /swapfile
$ sudo chmod 600 /swapfile
$ sudo mkswap /swapfile
$ sudo swapon /swapfile
$ sudo swapon -s
```

To make the swap space permanent, add <code>/swapfile none swap sw 0 0</code> to <code>/etc/fstab</code>.

## Configure GitHub, Clone Repository, Run Migrations
Create local SSH keys, copy the resulting <code>/home/username/.ssh/id_rsa.pub</code> to your SSH keys in GitHub, and clone your existing repository.

```terminal
$ cd ~
$ ssh-keygen -t rsa -b 4096 -C "your@email.address"
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_rsa

$ cd /opt/projectname
$ mkdir projectname
$ cd projectname
$ git clone git@github.com:your-github-username/github-projectname.git .
```

Make sure your Django project's settings.py file is updated appropriately, and then create your local database and run makemigrations/migrate.
```terminal
$ sudo su - postgres
postgres$ createuser dbadmin
postgres$ createdb projectdb --owner dbadmin
postgres$ psql -d projectdb
```
```sql
projectdb# ALTER USER dbadmin WITH PASSWORD 'xxxxx';
projectdb# ALTER ROLE dbadmin SET client_encoding TO 'utf8';
projectdb# ALTER ROLE dbadmin SET default_transaction_isolation to 'read committed';
projectdb# ALTER ROLE dbadmin SET timezone TO 'UTC';
projectdb# GRANT ALL PRIVILEGES ON DATABASE projectdb TO dbadmin;
projectdb# \q
postgres$ exit
```

Make sure you're inside your python environment and run makemigrations/migrate.
```terminal
$ source /opt/projectname/bin/activate
$ cd /opt/projectname/projectname
$ python manage.py makemigrations
$ python manage.py migrate
```

## Configure Gunicorn, NGINX, & Supervisor
### /etc/nginx/sites-available/projectname
NGINX configuration file -- some of the referenced files below will only be available after configuring Certbot in the next step. NGINX serves media files (images, CSS, etc) directly from the file system.

```nginx
upstream app_server {
    server unix:/opt/kairozu/run/gunicorn.sock fail_timeout=0;
}
server {
    listen 80;
    listen 443 ssl;
    server_name _ default;
    ssl_certificate /etc/nginx/ssl/nginx.crt;
    ssl_certificate_key /etc/nginx/ssl/nginx.key;
    return 444;
}
server {
    server_name project-domain-name.com;
    keepalive_timeout 5;
    client_max_body_size 4G;
    access_log /opt/projectname/logs/nginx-access.log;
    error_log /opt/projectname/logs/nginx-error.log;
    location /static/ {
        alias /opt/projectname/projectname/staticfiles/;
	    expires 30d;
    }
    location /.well-known {
        alias /opt/projectname/cert/.well-known;
    }
    location / {
        try_files $uri @proxy_to_app;
    }
    location @proxy_to_app {
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      proxy_redirect off;
      proxy_pass http://app_server;
    }
    listen 443 ssl; 
    ssl_certificate /etc/letsencrypt/live/project-domain-name.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/project-domain-name.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}
server {
    if ($host = project-domain-name.com) {
        return 301 https://$host$request_uri;
    }
    listen 80;
    server_name project-domain-name.com;
    return 404; 
}
```

After creating the NGINX config file, run the following:
```terminal
$ sudo chown root:root /etc/nginx/sites-available/kairozu
$ sudo ln -s /etc/nginx/sites-available/projectname /etc/nginx/sites-enabled/projectname
$ sudo rm /etc/nginx/sites-enabled/default
```

### /opt/projectname/bin/gunicorn_start
Gunicorn configuration file. Gunicorn creates a Unix socket and serves responses to NGINX via the WSGI protocol.

```bash
#!/bin/bash
NAME="projectname"
DIR=/opt/projectname/projectname
USER=username
GROUP=groupname
WORKERS=3
BIND=unix:/opt/kairozu/run/gunicorn.sock
DJANGO_SETTINGS_MODULE=kairozu.settings
DJANGO_WSGI_MODULE=kairozu.wsgi
LOG_LEVEL=error

cd $DIR
source ../bin/activate
export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
export PYTHONPATH=$DIR:$PYTHONPATH

exec ../bin/gunicorn ${DJANGO_WSGI_MODULE}:application \
  --name $NAME \
  --workers $WORKERS \
  --user=$USER \
  --group=$GROUP \
  --bind=$BIND \
  --log-level=$LOG_LEVEL \
  --log-file=-
```

Make this file executable and create a directory for the Unix socket file:
```terminal
$ chmod u+x gunicorn_start
$ mkdir /opt/projectname/run
```

### /etc/supervisor/conf.d/kairozu.conf
Supervisor configuration file -- after creating this file, run <code>chown root:root /etc/supervisor/conf.d/kairozu.conf</code> to change the owner to root.

```conf
[program:projectname]
command=/opt/projectname/bin/gunicorn_start
user=username
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/opt/projectname/logs/gunicorn-error.log
```

## Install & Configure Certbot
Certbot is "an easy-to-use automatic client that fetches and deploys SSL/TLS certificates for your web server." We follow the instructions for <a href="https://certbot.eff.org/lets-encrypt/debianstretch-nginx">NGINX on Debian 9 (stretch)</a>.

Add the line <code>deb http://ftp.debian.org/debian stretch-backports main</code> to the file <code>/etc/apt/sources.list.d/backports.list</code> and then run the following. After certbot, the additional keys are to prevent issues with nginx serving http requests.
```terminal
$ sudo apt-get update
$ sudo apt-get install python-certbot-nginx -t stretch-backports
$ sudo certbot --nginx

$ sudo mkdir /etc/nginx/ssl
$ sudo openssl req -x509 -nodes -days 3650 -newkey rsa:4096 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
```

Make sure you have appropriate <code>ssl_certificate</code>, <code>ssl_certificate_key</code> and <code>ssl_dhparam</code> values as seen in the <code>/etc/nginx/sites-available/projectname</code> file above. 

## Import Previous Data, Odds & Ends, Run!
First export the data from your local server/development postgres environment, then import the data into postgres on your server. Replace 'dbadmin' and 'projectdb' with your desired postgres username and database name from above as needed.
```terminal
Local:
$ sudo su - postgres
postgres$ pg_dump projectdb > project_db_backup.postgresqldb

Server:
$ sudo su - postgres
postgres$ dropdb projectdb
postgres$ createdb projectdb --owner dbadmin
postgres$ psql -d projectdb

projectdb# GRANT ALL PRIVILEGES ON DATABASE projectdb TO dbadmin;
projectdb# \q

postgres$ psql -d projectdb < /home/username/project_db_backup.postgresqldb
```

Create the log file directory and touch the initial log files for django and gunicorn.
```terminal
$ mkdir /opt/projectname/logs
$ touch /opt/projectname/logs/django.log
$ touch /opt/projectname/logs/gunicorn-error.log
```

Supervisor will start the application server/image if the server restarts. NGINX is the webserver which serves your files. This reloads everything to make sure you've reread the config files from above.
```terminal
$ sudo systemctl enable supervisor
$ sudo systemctl start supervisor
$ sudo supervisorctl reread
$ sudo supervisorctl update
$ sudo supervisorctl status projectname
$ sudo service nginx restart
```
