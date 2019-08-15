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
It took me some hours but it is a base64 image and it leads to /existence => https://darknetdiaries.com/existence/


## Problem 8 - /existence

That page gives me:

```
Some high stakes right here.
So what you waiting on?
Do you want to be here right now? And I don’t mean, like, here-here, but I mean here in a cosmic sense, bro.
Like, existence could be beautiful, or it could be ugly, but that’s on you.
How do you know which one’s for you?
You got to find out the future you’re fighting for.
Sometimes you got to close your eyes and really envision that stuff, bro.
If you like it, then it’s beautiful.


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
```

Another Base 64 string, tried to use as image again but it did not work
I could decipher it using base64 to string, but it gives a very strange binary file with a few HTTP request information, it seems like a binary communication. I discovered using hexdump that there is a part of the binary file that is a JPEG format, so I copy the hex data and there is just half of the picture, but from the extract from Mr Robot it seems /dream > http://darknetdiaries.com/dream
