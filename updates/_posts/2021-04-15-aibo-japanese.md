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
This is still a work in progress! The English given below is the English approximation of the Japanese command, not the literal English version of the command. The translations and phonetic attempts are best-effort, but many sounds and meanings don't have literal equivalents. Please let me know if you spot any errors.
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
        <td>わるいこ</td>
        <td>waruiko</td>
        <td>wah-rue-ee-ko</td>
        <td rowspan=8>scolding & discipline</td>
    </tr>
    <tr>
        <td>no no</td>
        <td>だめだめ</td>
        <td>damedame</td>
        <td>dah-may-dah-may</td>
    </tr>
    <tr>
        <td>no good</td>
        <td>だめよ</td>
        <td>dameyo</td>
        <td>dah-may-yo</td>
    </tr>
    <tr>
        <td>wrong</td>
        <td>ちがうよ</td>
        <td>chigauyo</td>
        <td>chi-gau-yo</td>
    </tr>
    <tr>
        <td>fool/dumb</td>
        <td>おばかさん</td>
        <td>obakasan</td>
        <td>oh-bah-ka-san</td>
    </tr>
    <tr>
        <td>fool/dumb</td>
        <td>おばか</td>
        <td>obaka</td>
        <td>oh-bah-ka</td>
    </tr>
    <tr>
        <td>hate</td>
        <td>きらい</td>
        <td>kirai</td>
        <td>key-rai</td>
    </tr>
    <tr>
        <td>bad at it</td>
        <td>へただね</td>
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
        <td>おて</td>
        <td>ote</td>
        <td>oh-tay</td>
        <td rowspan=2>shake hands, kinda looks like high five</td>
    </tr>
    <tr>
        <td>hand (do hand)</td>
        <td>おてして</td>
        <td>oteshite</td>
        <td>oh-tay-she-tay</td>
    </tr>
    <tr>
        <td>sit</td>
        <td>おすわり</td>
        <td>osuwari</td>
        <td>oh-sue-wah-ree</td>
        <td></td>
    </tr>
    <tr>
        <td>lie down</td>
        <td>ふせ</td>
        <td>fuse</td>
        <td>foo-say</td>
        <td></td>
    </tr>
    <tr>
        <td>sing</td>
        <td>うたって</td>
        <td>utatte</td>
        <td>ooh-tah-tay</td>
        <td>sing an aibo song</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>だんす</td>
        <td>dansu</td>
        <td>dah-n-sue</td>
        <td rowspan=3>do an aibo dance!</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>だんすして</td>
        <td>dansushite</td>
        <td>dah-n-sue-she-tay</td>
    </tr>
    <tr>
        <td>dance</td>
        <td>おどって</td>
        <td>odotte</td>
        <td>oh-doe-tay</td>
    </tr>
    <tr>
        <td>look over here</td>
        <td>こっちむいて</td>
        <td>kocchimuite</td>
        <td>ko-chi-moo-ee-tay</td>
        <td>aibo turns in direction of speaker and barks</td>
    </tr>
    <tr>
        <td>come here</td>
        <td>こっちおいで</td>
        <td>kocchioide</td>
        <td>ko-chi-oh-ee-day</td>
        <td rowspan=2>turn toward & walk to the speaker</td>
    </tr>
    <tr>
        <td>come here</td>
        <td>こっちきて</td>
        <td>kocchikite</td>
        <td>ko-chi-key-tay</td>
    </tr>
    <tr>
        <td>good night</td>
        <td>おやすみ</td>
        <td>oyasumi</td>
        <td>oh-yeah-sue-me</td>
        <td>go to sleep (not true sleep)</td>
    </tr>
    <tr>
        <td>wait</td>
        <td>まて</td>
        <td>mate</td>
        <td>ma-tay</td>
        <td>sit in one spot and wait (~30 mins)</td>
    </tr>
</tbody>
</table>
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
        <td>おぼえて</td>
        <td>oboete</td>
        <td>oh-bo-ay-tay</td>
        <td rowspan=2>takes the posture for learning a trick</td>
    </tr>
    <tr>
        <td>let's remember</td>
        <td>おぼえよう</td>
        <td>oboeyou</td>
        <td>oh-bo-ay-yo~</td>
    </tr>
    <tr>
        <td>remember?</td>
        <td>おぼえた？</td>
        <td>oboeta</td>
        <td>oh-bo-ay-tah?</td>
        <td rowspan=2>show the trick that has just been taught</td>
    </tr>
    <tr>
        <td>do you remember?</td>
        <td>おぼえたかな？</td>
        <td>oboetakana</td>
        <td>oh-bo-ay-tah-kah-na?</td>
    </tr>
    <tr>
        <td>don't forget</td>
        <td>わすれないでね</td>
        <td>wasurenaidene</td>
        <td>wah-sue-ray-nye-day-nay</td>
        <td>memorize the trick just taught</td>
    </tr>
    <tr>
        <td>do a remembered behavior</td>
        <td>おぼえたふるまいやって</td>
        <td>oboetafurumaiyatte</td>
        <td>oh-bo-ay-tah-foo-rue-mah-ee-yah-tay</td>
        <td>do one of the tricks which have been taught</td>
    </tr>
    <tr>
        <td>quit</td>
        <td>やめて</td>
        <td>yamete</td>
        <td>yah-may-tay</td>
        <td rowspan=2>stop doing the trick in progress</td>
    </tr>
    <tr>
        <td>stop</td>
        <td>とまれ</td>
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
        <td>しゃしんとって</td>
        <td>shashintotte</td>
        <td>sha-she-n-toe-tay</td>
        <td>look for a human face and take a photo</td>
    </tr>
    <tr>
        <td>take a photo (everyone)</td>
        <td>みんなのしゃしんをとって</td>
        <td>minnanoshashinwototte</td>
        <td>me-n-nah-no-sha-she-n-oh-toe-tay</td>
        <td>counts down and takes a photo (requires premium)</td>
    </tr>
    <tr>
        <td>take another</td>
        <td>もういちまい</td>
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
        <td>ちゃーじすてーしょん</td>
        <td>chaajisuteeshon</td>
        <td>chaa-jee-sue-tay-sho-n</td>
        <td rowspan=2>return to charging station</td>
    </tr>
    <tr>
        <td>go (re)charge</td>
        <td>じゅうでんして</td>
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
        <td>ほねとってきて</td>
        <td>honetottekite</td>
        <td>hoe-nay-toe-tay-key-tay</td>
        <td rowspan=2>pick up/play with aibone</td>
    </tr>
    <tr>
        <td>pick up aibone</td>
        <td>あいぼーんとってきて</td>
        <td>aiboontottekite</td>
        <td>ah-ee-bow-nn-toe-tay-key-tay</td>
    </tr>
    <tr>
        <td>throw bone</td>
        <td>ほねなげて</td>
        <td>honenagete</td>
        <td>hoe-nay-nah-gay-tay</td>
        <td rowspan=2>pick up aibone and throw it</td>
    </tr>
    <tr>
        <td>throw aibone</td>
        <td>あいぼーんなげて</td>
        <td>aiboonnagete</td>
        <td>ah-ee-bow-nn-nah-gay-tay</td>
    </tr>
    <tr>
        <td>kick the ball</td>
        <td>ぼーるけって</td>
        <td>boorukette</td>
        <td>bow-rue-kay-tay</td>
        <td>walk toward/kick the ball</td>
    </tr>
    <tr>
        <td>search for the ball</td>
        <td>ぼーるさがして</td>
        <td>boorusagashite</td>
        <td>bow-rue-sah-gah-she-tay</td>
        <td>look for the ball/bark when it is found</td>
    </tr>
    <tr>
        <td>dice color selection</td>
        <td>さいころいろえらび</td>
        <td>saikoroiroerabi</td>
        <td>sah-ee-ko-row-ee-row-ay-rah-bee</td>
        <td>not quite sure what this does yet</td>
    </tr> 
    <tr>
        <td>roll the dice</td>
        <td>さいころころがして</td>
        <td>saikorokorogashite</td>
        <td>sah-ee-ko-row-ko-row-gah-she-tay</td>
        <td>roll dice with front paw</td>
    </tr>
    <tr>
        <td>stack the dice</td>
        <td>さいころつんで</td>
        <td>saikorotsunde</td>
        <td>sah-ee-ko-row-tsu-n-day</td>
        <td>stacks one dice on top of the other</td>
    </tr>
    <tr>
        <td>throw the dice</td>
        <td>さいころなげて</td>
        <td>saikoronagete</td>
        <td>sah-ee-ko-row-nah-gay-tay</td>
        <td>pick up the dice and throw it</td>
    </tr>
    <tr>
        <td>bring the dice</td>
        <td>さいころもってきて</td>
        <td>saikoromottekite</td>
        <td>sah-ee-ko-row-mow-tay-key-tay</td>
        <td>pick up/bring the dice to you</td>
    </tr>
</tbody>
</table>