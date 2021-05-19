---
ID: 2818
post_title: >
  Working your magic with Firefox OS –
  Listen to orientation change
post_name: >
  working-your-magic-with-firefox-os-listen-to-orientation-change
author: Frédéric Harper
post_date: 2013-08-05 14:30:35
layout: post
link: >
  https://fred.dev/working-your-magic-with-firefox-os-listen-to-orientation-change/
published: true
tags:
  - working your magic with firefox os
categories:
  - Brainer
  - English
  - FIX ANTIDOTE
  - FIX IMAGE
  - FIX LANGUAGE
  - FIX TAGS
  - FIX URL
---
<figure><img src="http://fred.dev/wp-content/uploads/2013/08/FFxOS_Devs_twitterHeader_1252x626_1.png" alt="FFxOS_Devs_twitterHeader_1252x626_1" width="1252" height="626" /></figure>
One of the things I tried to do in the Firefox OS application I'm building is to manage the screen orientation. I want my application to know when the user changed the orientation of the phone, so I can take action accordingly. To do this, you need to listen to <em>onmozorientationchange</em>, and once it's called, you are able to know which orientation the phone is now: <em>portrait-primary</em>, <em>portrait-secondary</em>, <em>landscape-primary</em>, and <em>landscape-secondary</em>.

https://gist.github.com/fharper/6147153

It's now time for you to add this feature to your application.