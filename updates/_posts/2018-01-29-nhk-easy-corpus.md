---
layout: content
title: NHK Easy Corpus
tags: japanese code
---
I wanted to make a Japanese text corpus with a reading level somewhere on the lower end of the young adult range. NHK Easy News (aka NEWS WEB EASY) seems to be the gold standard for frequently updated, quality content specifically aimed at younger readers and those learning Japanese. The stories are written in short, easy sentences, with furigana above the kanji and dictionary popups on more complicated vocabulary. Alas, there's no easily accessible, complete archive.

<span class="smaller italics">Note: I love love love the NHK. Please pay your NHK reception fee (受信料) if you live in Japan. If you decide to pull text from the NHK Easy site, please be kind with your bandwidth demands, and don't abuse their site. Thanks. <3</span>

I sourced an NHK Easy archive from 2012-Current through a few different methods:
<ul>
<li>A messy archive via Google that covered 2012-2015, with the individual articles nested in a series of cluttered folders.</li>
<li>Using the <a href="https://cloud.google.com/bigquery/">Google BigQuery</a> public dataset of Reddit posts/comments to pull everything from 2015-June 2017 in the wonderful <a href="https://www.reddit.com/r/NHKEasyNews/">NHK Easy News Translation Subreddit</a> (NHKEasyNewsBot is a bot that automatically posts the text content of each article).</li>
<li>Writing a script to automatically pull and save new articles every 2-3 days.</li>
</ul>

This is the SQL statement for [Google BigQuery](https://cloud.google.com/bigquery/) if you want to download your own version of the second source. Note that this was 50.7 GB processed (which easily falls into the free tier for BigQuery, but be aware that BigQuery is not an otherwise free service). The results can be downloaded as a CSV file.
```sql
#standardSQL SELECT author, created_utc, url, title, selftext FROM `fh-bigquery.reddit_posts.201*` 
WHERE subreddit = 'NHKEasyNews' AND author = 'NHKEasyNewsBot'
```

To pull new NHK Easy articles every few days, I have an automated script which pulls article IDs from the site's JSON index of recent articles, downloads the appropriate html files, and saves the processed article IDs to a file.

The current URL format (as of February 24th, 2018) for NHK Easy articles is:
<code>http://www3.nhk.or.jp/news/easy/[ARTICLE ID]/[ARTICLE ID].html</code>, where [ARTICLE ID] is a unique identifier for each article. For example, the article found at <code>http://www3.nhk.or.jp/news/easy/k10011339591000/k10011339591000.html</code> would have an [ARTICLE ID] of k10011339591000.

This JSON file maintains an updated list of new NHK Easy articles: [http://www3.nhk.or.jp/news/easy/news-list.json](http://www3.nhk.or.jp/news/easy/news-list.json) -- this is where I pull article IDs from.

```python
# there are a few different ways to pull a file via http with python, but wget is quick and dirty
import wget

# keep a history of article IDs that've already been pulled so I don't pull them twice
with open('./nhkeasy/nhkeasy_retrieved_article_ids.txt', 'r') as f:
    retrieved_articleids = f.readlines()

retrieved_articleids = [x.strip() for x in retrieved_articleids]
add_to_retrieved = open('./nhkeasy/nhkeasy_retrieved_article_ids.txt', 'a')

# pull the new JSON list of article data from NHK
nhkjson = requests.get('http://www3.nhk.or.jp/news/easy/news-list.json').json()

for key, value in nhkjson[0].items():
    for x in value:
        if x['article_id'] in retrieved_articleids:
            # if the article ID has already been downloaded, skip it
            print("Already retrieved article with ID: " + x['article_id'])
        else:
            print("New article with ID: " + x['article_id'])
            add_to_retrieved.write("%s\n" % x['article_id'])
            nhkurl = 'http://www3.nhk.or.jp/news/easy/' + x['article_id'] + '/' + x['article_id'] + '.html'

            try:
                # download the new article and save it as an html file
                outputfilename = 'nhkeasy_' + x['article_id'] + '.html'
                filename = wget.download(geturl, out=outputfilename)
                print("Successful download of article ID: " + x['article_id'])
            except:
                print("Failed to download article ID: " + x['article_id'])
```

If you have a non-commercial interest in using the NHK Easy corpus I've built, I'm happy to share -- e-mail me at amber@kairozu.com and let me know what you'd be using it for.