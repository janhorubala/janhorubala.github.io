---
layout: default
title: SendMe
webpage: https://mixtube.co
cover: /assets/images/projects/mixtube_logo.png
description: Collaborative playlist for youtube parties!
---

Have you heard about digital photo frames? They're a combination of photo frame and tablet - an ordinary screen on which you can display photos. My grandma got one of these last holiday so she could be up to date with all the trips of my family members. But how to get photos on this device? Basically there are two ways. You can download the mobile application and send photos through this app, or you can configure the frame's email and send the photos manually via email.

So what was the problem? My grandma gets new photos very rarely. Not because no one took new photos - I saw thousands of them on my siblings' Facebook or Instagram.. But we didn’t remember to send them via the app. You know the situation: you take a perfect pic, put it on Facebook, on Instagram, maybe on a Snapchat but another app is too much! You just don’t remember to send it further.

That's why I decided to create a simple server that would fetch photos from social networks, and send them via email to my grandma's frame. But my girlfriend noticed that I didn’t need a server for that purpose. I can treat my grandmas mobile phone as a simple server - I need to synchronize the photo only once a day; my grandma has Wi-Fi most of the time, moreover she can force synchronization whenever she wants to check for new photos.

I chose React Native to write apps for Android, but I have several troubles due to the implementation. RN hasn’t got components for Alarm Manager and Background Workers. So I had to implement it on my own, I even open sourced these modules, you can check it out on my Github. Another problem was with sending emails, RN hasn’t got an email client, so I decided (for now) to use REST API provided by Gmail. I know it’s not ideal, but for my grandma it’s enough.

And last problem, more human related. To fetch other photos from Facebook and Instagram you need permission and all siblings boycotted the idea of sending my grandma all of their photos. I’m thinking about adding some filter by tags or something, but for now my grandma convinced everybody to approve the app.