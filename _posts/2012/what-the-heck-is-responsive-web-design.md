---
ID: 2991
post_title: What the heck is Responsive Web Design?
post_name: what-the-heck-is-responsive-web-design
author: Frédéric Harper
post_date: 2012-02-16 16:00:52
layout: post
link: >
  https://fred.dev/what-the-heck-is-responsive-web-design/
published: true
tags: [ ]
categories:
  - Brainer
  - English
  - FIX ANTIDOTE
  - FIX IMAGE
  - FIX LANGUAGE
  - FIX TAGS
  - FIX URL
---
<figure><img title="Responsive Web Design" alt="" src="http://fred.dev/wp-content/uploads/2012/02/5818096043_1995236700_o-580x400.jpg" width="580" height="400"/><figcaption> Creative Commons: https://www.flickr.com/photos/adactio/5818096043/</figcaption></figure><p align="justify"><span style="color:#333">As a Web developer, we need to think about many devices, screen sizes and orientations. It’s not enough now to build our application or website to target only desktop screens: you need to keep in mind that your visitors will come to your site with their smartphones, their netbooks, their tablets, their slates and even their living room TV. We need to give them a good experience.</span></p><p align="justify">Instead of creating a specific version for the most common screen resolution or for specific mobile experience, Responsive Web Design is all about creating an experience that will keep in mind the user’s needs instead of ours. Flexibility is the keyword as we adapt to various devices' capabilities, instead of configurations.</p><p align="justify">How many times did you tried to see a website that is not mobile-friendly? Everything is too big for the size of the screen. You have to zoom-in, zoom-out, and it’s very frustrating. With a fixed-width design, the owner will have to create a version for each device that their customers use.</p><p align="justify">So what is really this Responsive Design thing? It’s base on three technical aspects:</p><ol><li><div align="justify">Media queries</div></li><li><div align="justify">A flexible grid-based layout</div></li><li><div align="justify">Flexible images and media</div></li></ol><p align="justify"><strong>Media Queries</strong></p><p align="justify">Media queries are like having if statement in your CSS. You can define which CSS stylesheet will be loaded depending on different criteria, like the size of the screen. Everything is managed by the browser and there is no need to do like we did in the past with some JavaScript and page reloading. Here are some examples:</p><div align="justify"> <pre lang="css">	<link href="mobile.css" rel="stylesheet" media="screen and (max-width:480px)" type="text/css" />

	<link href="netbook.css" rel="stylesheet" media="screen and (min-width:481px)

<p>and (max-width: 1024px)" type="text/css" /> </p>

	<link href="laptop.css" rel="stylesheet" media="screen and (min-width:1025px)" type="text/css" /></pre></div><p align="justify"><strong>A flexible grid-bases layout</strong></p><p align="justify">Everybody loves pixels. We used pixels for a long time in the Web, and Designer loves them too. The problem is that the screen representation of a pixel is different  on every device or screens. The answers in using a flexible grid-bases layout reside in percentage or em for sizing. The idea is to use relative size for text, width and margins.</p><p align="justify"><strong>Flexible images and media</strong></p><p align="justify">The last part, but not the less important is about your media. The images and videos needs to be flexible too. It’s a basic principle that allows you to scale or shrink your media with CSS. You can also use a technique with alternate version of the media or sometimes, when it makes sense, no media at all.</p><p align="justify">If you want to see Responsive Web Design in action, you can go to <a title="https://mediaqueri.es/" href="https://mediaqueri.es/">https://mediaqueri.es/</a> that list some great examples. Use your smarthphone, your tablet or resize your desktop Web browser: you will see the magic of Responsive Web Design. This blog post is a good start to understand the idea behind it, but if you have an interest in this topic, I will be more than happy to make other blog posts to dive deeper into the subject. For those of you that can’t wait, one of the best book out there is the one from <a href="https://www.abookapart.com/products/responsive-web-design" target="_blank" rel="noopener noreferrer">A Book Apart</a>. Oh and if you are in Montreal, I’ll do a presentation on <a href="https://www.meetup.com/HTML5mtl/events/47958602/" target="_blank" rel="noopener noreferrer">Responsive Web Design (in French)</a> at <a href="https://www.meetup.com/HTML5mtl/" target="_blank" rel="noopener noreferrer">HTML5mtl</a> next week.</p><p align="justify"><strong>Do you think Responsive Web Design is the way to go? Do you already use it? Did you see amazing implementation of this technique on the Web? Share your thoughts.</strong></p><div id="cross-post">This blog post also appears in the <a href="https://blogs.msdn.com/b/cdnwebdevs/" target="_blank" rel="noopener noreferrer">Canadian Web Developer blog</a></div>