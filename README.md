# Solving Darknet Diaries Problem

## Problem 1 - Podcast Easter Egg

* Episode 1: A voice say the following: B2 A1 E5 G7 C3 H8 D4 F6 E5
* Episode 2: Morse code that gives: A1 A5 A6 B1 B4 B7 C1 C4 C7 D2 D3 D6
* Episode 3: At the end we can reverse the audio and it gives us A1 A2 A3 A4 A5 B1 B3 B5 B1 E5
* Episode 4: A voice says the folling numbers: 97 50 32 97 51 32 97 52 32 98 49 32 98 53 32 99 49 32 99 53 32 100 50 32 100 52, using ASCII table we have A2 A3 A4 B1 B5 C1 C5 D2 D4
* Episode 5: Couldn't find any clue =/
* Epsiode 6: Strange sound that analysed in an audio program gives: A1 A2 A3 A4 A5 B1 B3 B5 E1 E5 
* Epsiode 7: There's A5 B1 B2 B3 B4 B5 C5 B4 

We can put in a board with columns A,B,C,D,E,F,G,H and lines 1 to 7, each episode gives an image that leads to /secet, as the Episode 5 is missing I suppose we have /secret, which leads to https://darknetdiaries.com/secret/


## Problem 2 - /secret

When I downloaded the image and run tail on it, I'm able to see at the end of the file "Your move 2bd87cf22c40d4aa65a2e747ab8988a4"

2bd87cf22c40d4aa65a2e747ab8988a4 seems like a hash so I run it against  https://hashkiller.co.uk/Cracker and it gives me:
"2bd87cf22c40d4aa65a2e747ab8988a4 MD5 chessmaster" which leads to https://darknetdiaries.com/chessmaster/

## Problem 3 - /chessmaster

Opening the source code we can see
<!-- The only way to patch a vulnerability is by exposing it first. How do I know you aren't a robot or anything? -->
Tried a brute force approach to found some robot directory exposed and it gives me https://darknetdiaries.com/robots.txt


## Problem 4 - /robots.txt

We have the following:
```
User-agent: *
Disallow: /js/
Disallow: /css/
Disallow: /0x784251/
Sitemap: https://darknetdiaries.com/sitemap.xml
```

And I can access https://darknetdiaries.com/0x784251/

## Problem 5 - /0x784251

Opening the source code of the page we can see the JS function and it gives a clue that if we put "Winner takes all of what?" and click submit that browser show us "/us" which leads to https://darknetdiaries.com/us


## Problem 6 - /us

We can look at the source code in find a strange function if we copy everything inside the eval() we have:

```
function(p,a,c,k,e,d){e=function(c){return c.toString(36)};if(!''.replace(/^/,String)){while(c--){d[c.toString(a)]=k[c]||c.toString(a)}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('1 3="a b c 9 8 4";1 2=6.7("d").e;k(3==2){j(i(\'/%f%0%0%g%h%n%m%l%5%0\'))}',24,24,'6E|var|input|chat|logic|69o|document|getElementById|the|see|I|fail|to|key|value|61|69|68|decodeURI|alert|if|74|61|69l'.split('|'),0,{})
```

Putting it in the console we have "var chat="I fail to see the logic";var input=document.getElementById("key").value;if(chat==input){alert(decodeURI('/%61%6E%6E%69%68%69l%61%74%69o%6E'))}". So if we put "I fail to see the logic" and click on submit that browser gives us /annihilation => https://darknetdiaries.com/annihilation


## Problem 7 - /annihilation

We have a page with the following text 

```
So what you playing for then? If there's no who, then what's the what? What's it for? 

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
```
I could not crack it yet I just know for now that it has a lot of / and + that could leads me to the clue, seems like a .pem key

The text it's from Mr Robot:

esp2.2_init_1.asec
```
Elliot: Asking for help was never Darlene's strong suit, but then again is it anyone's? An admission of weakness. But you can't avoid the simple truth - the only way to patch a vulnerability is by exposing it first. The flip side being that exposing the vulnerability leaves you open for an exploit.
Mr. Robot: You wanna unburden yourself, go jerk off. This is a road paved with your dead friends and family.
Elliot: Annihilation is always the answer. We destroy parts of ourselves everyday. We photoshop our warts away, we edit the parts we hate about ourselves, modify the parts we think people hate. We curate our identity, carve it, distill it. Krista's wrong - annihilation is all we are.
Cisco: We're past fragile. The shit that we're in is fucking shattered into a million little pieces.
Darlene: You wanna help? Be a man and let me be upset.
Leon: You know, back in the age of Enlightenment, mo'fuckers used chess as a means of self improvement, 'cuz there wasn't no Tony Robbins DVDs back then - this was it. So what you playin' for then? If there's no who, then what's the what? What's it for?
Elliot: Existence.
Leon: Dope, that's some high stakes right there. So what you waitin' on?
Elliot: What?
Leon: Do you dream Elliot? You scrapin' so hard like you ain't never asked yourself this before. I said do you wanna be here right now? And I don't mean like here here, I mean like here in a cosmic sense, bro. Like, existence could be beautiful, or it could be ugly, but that's on you.
Elliot: How do I know which one is for me?
Leon: Dream. You gotta find out the future you're fightin' for. Sometimes you gotta close your eyes and really envision that shit, bro. If you like it, then it's beautiful; if you don't, then you might as well fade the fuck out right now.
Ray: Did you know that Moses heard voices too? Abraham, John, Paul, Jesus. In fact, many prophets confessed to hearing voices. People like you, what you have, it can be divinity, Elliot, if you let it.
```
