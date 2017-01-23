---
layout: post
title: 4HP: DeviantArt Tinder Game
comments: true
---

4HP (4 Hour Project) is a series of simple tasks implemented in 2-4 hours. The main reason is to learn something new, try hot technology or make small research and pickup the best framework/lib.

### Foundation
Last week I had a small argue with my brother. We talked about photography business. My brother claimed that his friends is one of the best photographer and his photos are just amazing. I was trying to find out what makes his friend outstanding.
We couldn’t get any conclusions, so I decided to implement simple game that will show if there is some special difference between random photos and photos from his friend’s portfolio. I found out that his friend has a profile on DeviantArt and DeviantArt has an open API. The continuation was simple - I fetched his friends photos, mixed them with newest and random photos from DeviantArt and display them in tinder-like gallery: if you claim that photo is taken by friend - swipe to right, otherwise - swipe to left.
My brother couldn’t get a 100% score and I treat it as my little victory. After all I added ability to choose deviant and play in one versus another game (for example to check if you can recognize a unique style of your favorite photographer).

[DEMO](http://jonzee.me/deviantart/)

### Instructions
On mobile you can swipe photos left or right, on desktop use arrows (left/right) to swipe photos). Click on profile picture to change user with nickname.

### Technology
- [jTinder](https://github.com/do-web/jTinder) - jQuery plugin for tinder-like cards, first result, works at first run, nothing to add, [example](http://netcup-gutschein.x5c.de/jtinder/)
- [ProgressBar.js](https://github.com/kimmobrunfeldt/progressbar.js) - I choose this lib from > 50 others, it has greatest design and functionality that I was looking for (changing colors), [examples](https://kimmobrunfeldt.github.io/progressbar.js/)
- [DeviantArt Gallery Plugin](https://github.com/jamesl1001/deviantART-Gallery-Plugin) - 
- [YQL](https://developer.yahoo.com/yql/) - Yahoo Query Langauge

### What I learned
- [Fisher-Yates Shuffle](https://bost.ocks.org/mike/shuffle/) - I was looking for some algorithm to shuffle photos in array (to not display the same photo in every game), I choose Fisher-Yates
- YQL - Yahoo Query Langauge yahooapis that change xml to json (which is nice) "http://query.yahooapis.com/v1/public/yql?q=" + escape('select * from xml where url="' + url + '"') + "&_maxage=86400&format=json&callback=callback""
- DeviantArt API - is pretty strange, never used RSS API before
