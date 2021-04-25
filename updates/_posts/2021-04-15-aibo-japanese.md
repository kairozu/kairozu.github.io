---
layout: content
title: Japanese Aibo Commands
tags: update code japan japanese project
---
<style>
table, th, td {
    border: 1px solid #506D85;
    padding: 2px 5px;
}
table { 
    border-collapse: collapse;
    width: 100%;
}
</style>
<script>
function play(sound) {
    var audio = document.getElementById(sound);
    audio.play();
}
</script>
This is still a work in progress! The English given below is the English approximation of the Japanese command, <b>not the literal English version of the command</b>. The translations and phonetic attempts are best-effort, but many sounds and meanings don't have literal equivalents. Please let me know if you spot any errors.
<br /><br />
To Do: add ~50 more commands, verify commands which do/don't require cloud access, verify commands which do/don't require premium access
<br />
<h4>気持ち / kimochi / feelings (praise & scolding)</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>good girl/boy</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('iiko')">
        <audio id="iiko" src="/sounds/iiko.mp3"></audio>
        いいこ
        </td>
        <td>iiko</td>
        <td>eeee-ko</td>
        <td rowspan=10>praise & compliments</td>
    </tr>
    <tr>
        <td>well-behaved</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('orikou')">
        <audio id="orikou" src="/sounds/orikou.mp3"></audio>
        おりこう</td>
        <td>orikou</td>
        <td>oh-ree-ko</td>
    </tr>
    <tr>
        <td>good job/there there</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('yoshiyoshi')">
        <audio id="yoshiyoshi" src="/sounds/yoshiyoshi.mp3"></audio>
        よしよし</td>
        <td>yoshiyoshi</td>
        <td>yo-sh-yo-sh</td>
    </tr>
    <tr>
        <td>amazing</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('sugoi')">
        <audio id="sugoi" src="/sounds/sugoi.mp3"></audio>
        すごい</td>
        <td>sugoi</td>
        <td>sue-go-ee</td>
    </tr>
    <tr>
        <td>as expected (good)</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('sasugadane')">
        <audio id="sasugadane" src="/sounds/sasugadane.mp3"></audio>
        さすがだね</td>
        <td>sasugadane</td>
        <td>saw-sue-gah-dah-nay</td>
    </tr>
    <tr>
        <td>thank you</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('arigatou')">
        <audio id="arigatou" src="/sounds/arigatou.mp3"></audio>
        ありがとう</td>
        <td>arigatou</td>
        <td>ah-ree-gah-toe</td>
    </tr>
    <tr>
        <td>do your best</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('ganbare')">
        <audio id="ganbare" src="/sounds/ganbare.mp3"></audio>
        がんばれ</td>
        <td>ganbare</td>
        <td>gah-n-bah-ray</td>
    </tr>
    <tr>
        <td>congrats</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('omedetou')">
        <audio id="omedetou" src="/sounds/omedetou.mp3"></audio>
        おめでとう</td>
        <td>omedetou</td>
        <td>oh-may-day-toe</td>
    </tr>
    <tr>
        <td>well done</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('yokuyatta')">
        <audio id="yokuyatta" src="/sounds/yokuyatta.mp3"></audio>
        よくやった</td>
        <td>yokuyatta</td>
        <td>yo-ku-yah-tah</td>
    </tr>
    <tr>
        <td>love you</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('suki')">
        <audio id="suki" src="/sounds/suki.mp3"></audio>
        すき</td>
        <td>suki</td>
        <td>sue-key</td>
    </tr>
    <tr>
        <td>bad girl/boy</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('waruiko')">
        <audio id="waruiko" src="/sounds/waruiko.mp3"></audio>
        わるいこ</td>
        <td>waruiko</td>
        <td>wah-rue-ee-ko</td>
        <td rowspan=8>scolding & discipline</td>
    </tr>
    <tr>
        <td>no no</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('damedame')">
        <audio id="damedame" src="/sounds/damedame.mp3"></audio>
        だめだめ</td>
        <td>damedame</td>
        <td>dah-may-dah-may</td>
    </tr>
    <tr>
        <td>no good</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('dameyo')">
        <audio id="dameyo" src="/sounds/dameyo.mp3"></audio>
        だめよ</td>
        <td>dameyo</td>
        <td>dah-may-yo</td>
    </tr>
    <tr>
        <td>wrong</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('chigauyo')">
        <audio id="chigauyo" src="/sounds/chigauyo.mp3"></audio>
        ちがうよ</td>
        <td>chigauyo</td>
        <td>chi-gau-yo</td>
    </tr>
    <tr>
        <td>fool/dumb</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('obakasan')">
        <audio id="obakasan" src="/sounds/obakasan.mp3"></audio>
        おばかさん</td>
        <td>obakasan</td>
        <td>oh-bah-ka-san</td>
    </tr>
    <tr>
        <td>fool/dumb</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('obaka')">
        <audio id="obaka" src="/sounds/obaka.mp3"></audio>
        おばか</td>
        <td>obaka</td>
        <td>oh-bah-ka</td>
    </tr>
    <tr>
        <td>hate</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('kirai')">
        <audio id="kirai" src="/sounds/kirai.mp3"></audio>
        きらい</td>
        <td>kirai</td>
        <td>key-rai</td>
    </tr>
    <tr>
        <td>bad at it</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('hetadane')">
        <audio id="hetadane" src="/sounds/hetadane.mp3"></audio>
        へただね</td>
        <td>hetadane</td>
        <td>hey-tah-dah-nay</td>
    </tr>
</tbody>
</table>
<h4>ふるまい / furumai / behavior</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>hand</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('ote')">
        <audio id="ote" src="/sounds/ote.mp3"></audio>
        おて</td>
        <td>ote</td>
        <td>oh-tay</td>
        <td rowspan=2>shake hands, kinda looks like high five</td>
    </tr>
    <tr>
        <td>hand (do hand)</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oteshite')">
        <audio id="oteshite" src="/sounds/oteshite.mp3"></audio>
        おてして</td>
        <td>oteshite</td>
        <td>oh-tay-she-tay</td>
    </tr>
    <tr>
        <td>sit</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('osuwari')">
        <audio id="osuwari" src="/sounds/osuwari.mp3"></audio>
        おすわり</td>
        <td>osuwari</td>
        <td>oh-sue-wah-ree</td>
        <td></td>
    </tr>
    <tr>
        <td>lie down</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('fuse')">
        <audio id="fuse" src="/sounds/fuse.mp3"></audio>
        ふせ</td>
        <td>fuse</td>
        <td>foo-say</td>
        <td></td>
    </tr>
    <tr>
        <td>sing</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('utatte')">
        <audio id="utatte" src="/sounds/utatte.mp3"></audio>
        うたって</td>
        <td>utatte</td>
        <td>ooh-tah-tay</td>
        <td>sing an aibo song</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('dansu')">
        <audio id="dansu" src="/sounds/dansu.mp3"></audio>
        だんす</td>
        <td>dansu</td>
        <td>dah-n-sue</td>
        <td rowspan=3>do an aibo dance!</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('dansushite')">
        <audio id="dansushite" src="/sounds/dansushite.mp3"></audio>
        だんすして</td>
        <td>dansushite</td>
        <td>dah-n-sue-she-tay</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('odotte')">
        <audio id="odotte" src="/sounds/odotte.mp3"></audio>
        おどって</td>
        <td>odotte</td>
        <td>oh-doe-tay</td>
    </tr>
    <tr>
        <td>look over here</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('kocchimuite')">
        <audio id="kocchimuite" src="/sounds/kocchimuite.mp3"></audio>
        こっちむいて</td>
        <td>kocchimuite</td>
        <td>ko-chi-moo-ee-tay</td>
        <td>aibo turns in direction of speaker and barks</td>
    </tr>
    <tr>
        <td>come here</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('kocchioide')">
        <audio id="kocchioide" src="/sounds/kocchioide.mp3"></audio>
        こっちおいで</td>
        <td>kocchioide</td>
        <td>ko-chi-oh-ee-day</td>
        <td rowspan=2>turn toward & walk to the speaker</td>
    </tr>
    <tr>
        <td>come here</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('kocchikite')">
        <audio id="kocchikite" src="/sounds/kocchikite.mp3"></audio>
        こっちきて</td>
        <td>kocchikite</td>
        <td>ko-chi-key-tay</td>
    </tr>
    <tr>
        <td>good night</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oyasumi')">
        <audio id="oyasumi" src="/sounds/oyasumi.mp3"></audio>
        おやすみ</td>
        <td>oyasumi</td>
        <td>oh-yeah-sue-me</td>
        <td>go to sleep (few mins; not true sleep)</td>
    </tr>
    <tr>
        <td>wait</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('matte')">
        <audio id="matte" src="/sounds/matte.mp3"></audio>
        まて</td>
        <td>mate</td>
        <td>ma-tay</td>
        <td>sit in one spot and wait (few mins)</td>
    </tr>
</tbody>
</table>
<h4>ふるまい / furumai / behavior - settle down mode</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>don't move (settle down)</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('osumashisan')">
        <audio id="osumashisan" src="/sounds/osumashisan.mp3"></audio>
        おすましさん</td>
        <td>osumashisan</td>
        <td>oh-sue-ma-she-san</td>
        <td rowspan=2>aibo will raise a paw; press it and stroke head or back at the same time</td>
    </tr>
    <tr>
        <td>it's ok to move</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('ugoiteiiyo')">
        <audio id="ugoiteiiyo" src="/sounds/ugoiteiiyo.mp3"></audio>
        うごいていいよ</td>
        <td>ugoiteiiyo</td>
        <td>ooh-go-ee-tay-ee-yo</td>
    </tr>
</tbody>
</html>
<h4>ふるまい / furumai / behavior - memory</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>remember</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oboete')">
        <audio id="oboete" src="/sounds/oboete.mp3"></audio>
        おぼえて</td>
        <td>oboete</td>
        <td>oh-bo-ay-tay</td>
        <td rowspan=2>takes the posture for learning a trick</td>
    </tr>
    <tr>
        <td>let's remember</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oboeyou')">
        <audio id="oboeyou" src="/sounds/oboeyou.mp3"></audio>
        おぼえよう</td>
        <td>oboeyou</td>
        <td>oh-bo-ay-yo~</td>
    </tr>
    <tr>
        <td>remember?</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oboeta')">
        <audio id="oboeta" src="/sounds/oboeta.mp3"></audio>
        おぼえた？</td>
        <td>oboeta</td>
        <td>oh-bo-ay-tah?</td>
        <td rowspan=2>show the trick that has just been taught</td>
    </tr>
    <tr>
        <td>do you remember?</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oboetakana')">
        <audio id="oboetakana" src="/sounds/oboetakana.mp3"></audio>
        おぼえたかな？</td>
        <td>oboetakana</td>
        <td>oh-bo-ay-tah-kah-na?</td>
    </tr>
    <tr>
        <td>don't forget</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('wasurenaidene')">
        <audio id="wasurenaidene" src="/sounds/wasurenaidene.mp3"></audio>
        わすれないでね</td>
        <td>wasurenaidene</td>
        <td>wah-sue-ray-nye-day-nay</td>
        <td>memorize the trick just taught</td>
    </tr>
    <tr>
        <td>do a remembered behavior</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('oboetafurumaiyatte')">
        <audio id="oboetafurumaiyatte" src="/sounds/oboetafurumaiyatte.mp3"></audio>
        おぼえたふるまいやって</td>
        <td>oboetafurumaiyatte</td>
        <td>oh-bo-ay-tah-foo-rue-mah-ee-yah-tay</td>
        <td>do one of the tricks which have been taught</td>
    </tr>
    <tr>
        <td>quit</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('yamete')">
        <audio id="yamete" src="/sounds/yamete.mp3"></audio>
        やめて</td>
        <td>yamete</td>
        <td>yah-may-tay</td>
        <td rowspan=2>stop doing the trick in progress</td>
    </tr>
    <tr>
        <td>stop</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('tomare')">
        <audio id="tomare" src="/sounds/tomare.mp3"></audio>
        とまれ</td>
        <td>tomare</td>
        <td>toe-ma-ray</td>
    </tr>
</tbody>
</table>
<h4>ふるまい / furumai / behavior - photos</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>take a photo</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('shashintotte')">
        <audio id="shashintotte" src="/sounds/shashintotte.mp3"></audio>
        しゃしんとって</td>
        <td>shashintotte</td>
        <td>sha-she-n-toe-tay</td>
        <td>look for a human face and take a photo</td>
    </tr>
    <tr>
        <td>take a photo (everyone)</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('minnanoshashinwototte')">
        <audio id="minnanoshashinwototte" src="/sounds/minnanoshashinwototte.mp3"></audio>
        みんなのしゃしんをとって</td>
        <td>minnanoshashinwototte</td>
        <td>me-n-nah-no-sha-she-n-oh-toe-tay</td>
        <td>counts down and takes a photo (requires premium)</td>
    </tr>
    <tr>
        <td>take another</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('mouichimai')">
        <audio id="mouichimai" src="/sounds/mouichimai.mp3"></audio>
        もういちまい</td>
        <td>mouichimai</td>
        <td>mow-ee-chi-ma-ee</td>
        <td>take another photo (requires premium)</td>
    </tr>
</tbody>
</table>
<h4>ふるまい / furumai / behavior - battery</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>charging station</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('chaajisuteeshon')">
        <audio id="chaajisuteeshon" src="/sounds/chaajisuteeshon.mp3"></audio>
        ちゃーじすてーしょん</td>
        <td>chaajisuteeshon</td>
        <td>chaa-jee-sue-tay-sho-n</td>
        <td rowspan=2>return to charging station</td>
    </tr>
    <tr>
        <td>go (re)charge</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('juudenshite')">
        <audio id="juudenshite" src="/sounds/juudenshite.mp3"></audio>
        じゅうでんして</td>
        <td>juudenshite</td>
        <td>jew-day-n-she-tay</td>
    </tr>
</tbody>
</table>

<h4>ふるまい / furumai / behavior - toys</h4>
<table>
<thead>
    <tr>
        <th>
            English
        </th>
        <th>
            Japanese (hiragana)
        </th>
        <th>
            Japanese (roman)
        </th>
        <th>
            English phonetic
        </th>
        <th>
            English notes
        </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>pick up bone</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('honetottekite')">
        <audio id="honetottekite" src="/sounds/honetottekite.mp3"></audio>
        ほねとってきて</td>
        <td>honetottekite</td>
        <td>hoe-nay-toe-tay-key-tay</td>
        <td rowspan=2>pick up/play with aibone</td>
    </tr>
    <tr>
        <td>pick up aibone</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('aiboontottekite')">
        <audio id="aiboontottekite" src="/sounds/aiboontottekite.mp3"></audio>
        あいぼーんとってきて</td>
        <td>aiboontottekite</td>
        <td>ah-ee-bow-nn-toe-tay-key-tay</td>
    </tr>
    <tr>
        <td>throw bone</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('honenagete')">
        <audio id="honenagete" src="/sounds/honenagete.mp3"></audio>
        ほねなげて</td>
        <td>honenagete</td>
        <td>hoe-nay-nah-gay-tay</td>
        <td rowspan=2>pick up aibone and throw it</td>
    </tr>
    <tr>
        <td>throw aibone</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('aiboonnagete')">
        <audio id="aiboonnagete" src="/sounds/aiboonnagete.mp3"></audio>
        あいぼーんなげて</td>
        <td>aiboonnagete</td>
        <td>ah-ee-bow-nn-nah-gay-tay</td>
    </tr>
    <tr>
        <td>kick the ball</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('boorukette')">
        <audio id="boorukette" src="/sounds/boorukette.mp3"></audio>
        ぼーるけって</td>
        <td>boorukette</td>
        <td>bow-rue-kay-tay</td>
        <td>walk toward/kick the ball</td>
    </tr>
    <tr>
        <td>search for the ball</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('boorusagashite')">
        <audio id="boorusagashite" src="/sounds/boorusagashite.mp3"></audio>
        ぼーるさがして</td>
        <td>boorusagashite</td>
        <td>bow-rue-sah-gah-she-tay</td>
        <td>look for the ball/bark when it is found</td>
    </tr>
    <tr>
        <td>dice color selection</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('saikoroiroerabi')">
        <audio id="saikoroiroerabi" src="/sounds/saikoroiroerabi.mp3"></audio>
        さいころいろえらび</td>
        <td>saikoroiroerabi</td>
        <td>sah-ee-ko-row-ee-row-ay-rah-bee</td>
        <td>not quite sure what this does yet</td>
    </tr> 
    <tr>
        <td>roll the dice</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('saikorokorogashite')">
        <audio id="saikorokorogashite" src="/sounds/saikorokorogashite.mp3"></audio>
        さいころころがして</td>
        <td>saikorokorogashite</td>
        <td>sah-ee-ko-row-ko-row-gah-she-tay</td>
        <td>roll dice with front paw</td>
    </tr>
    <tr>
        <td>stack the dice</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('saikorotsunde')">
        <audio id="saikorotsunde" src="/sounds/saikorotsunde.mp3"></audio>
        さいころつんで</td>
        <td>saikorotsunde</td>
        <td>sah-ee-ko-row-tsu-n-day</td>
        <td>stacks one dice on top of the other</td>
    </tr>
    <tr>
        <td>throw the dice</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('saikoronagete')">
        <audio id="saikoronagete" src="/sounds/saikoronagete.mp3"></audio>
        さいころなげて</td>
        <td>saikoronagete</td>
        <td>sah-ee-ko-row-nah-gay-tay</td>
        <td>pick up the dice and throw it</td>
    </tr>
    <tr>
        <td>bring the dice</td>
        <td>
        <input type="button" value="&#9658;" onclick="play('saikoromottekite')">
        <audio id="saikoromottekite" src="/sounds/saikoromottekite.mp3"></audio>
        さいころもってきて</td>
        <td>saikoromottekite</td>
        <td>sah-ee-ko-row-mow-tay-key-tay</td>
        <td>pick up/bring the dice to you</td>
    </tr>
</tbody>
</table>