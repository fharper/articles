---
ID: 2823
post_title: 'Working your magic with Firefox OS &#8211; Playing mp4'
post_name: >
  working-your-magic-with-firefox-os-playing-mp4
author: Frédéric Harper
post_date: 2013-07-30 19:42:13
layout: post
link: >
  https://fred.dev/working-your-magic-with-firefox-os-playing-mp4/
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
<figure><img src="http://fred.dev/wp-content/uploads/2013/07/FFxOS_Devs_twitterHeader_1252x626_1.png" alt="FFxOS_Devs_twitterHeader_1252x626_1" width="1252" height="626" /></figure>
Everything you are looking for, about Firefox OS development, is either on the <a href="https://marketplace.firefox.com/developers/" target="_blank" rel="noopener noreferrer">Firefox MarketPlace Developer Hub</a> or on the <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Firefox_OS?menu" target="_blank" rel="noopener noreferrer">Mozilla Developer Network</a>. We are also publishing blog posts on our blog, <a href="https://hacks.mozilla.org/" target="_blank" rel="noopener noreferrer">Mozilla Hacks</a>, and I will do it also. Once in a while, I come with questions or code examples I want to share that doesn't really fit in the hacks blog for different reasons. In that situation, I'll use my own blog to share with you some of this stuff. Because I like posts series, this one will be named "<a href="http://fred.dev/tag/working-your-magic-with-firefox-os/">Working your magic with Firefox OS</a>".

For the first one, I got an interesting question from a developer last week. He was asking if it's possible to play mp4 in a Firefox OS application. The answer is yes, and no. You cannot play a mp4 in the &lt;video&gt; tag for security reason, but there is another way to do it: Web Activity. By using this sample code below, you will be able to play a mp4 file.

https://gist.github.com/fharper/6091404

Keep in mind that for now, it's not working in the simulator, and it also depends on the codecs on a real device. As an example, it wasn't working with a file using isom, but it worked well with one using mp42 codec.