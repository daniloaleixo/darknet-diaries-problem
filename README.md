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
User-agent: *
Disallow: /js/
Disallow: /css/
Disallow: /0x784251/
Sitemap: https://darknetdiaries.com/sitemap.xml

And I can access https://darknetdiaries.com/0x784251/



