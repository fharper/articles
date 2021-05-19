---
ID: 2846
post_title: 'HTML5 Challenge #1 &#8211; The result'
post_name: html5-challenge-1-the-result
author: Frédéric Harper
post_date: 2013-05-16 14:00:19
layout: post
link: >
  https://fred.dev/html5-challenge-1-the-result/
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
<del datetime="2013-05-15T01:12:00+00:00">Two weeks</del> One month (I decided to give one month as requested by many people) have passed since I put the <a title="HTML5 challenge #1 – Canvas &amp; File API" href="https://fred.dev/html5-challenge-1-canvas-file-api/">first challenge</a> online, so it's now the time to show you my solution. On one side, for my own pleasure, I wanted to give a more than complete solution with many options, or different ways to do it. On the other side, too often I saw examples about a specific element of a programming language that were too complex. If you were a new developer, you can get lost easily with all the code just to find what you were looking for, so I decided to take the simpler path.

Because I know how the Internet is working, let me also specify that this is not considered as the ultimate, and perfect solution: this is the solution I made with my knowledges, and I will be more than happy to discuss it in the comment section. The last thing to take into consideration before we start: I suck with design, and it's OK as the goal is not to have something pretty, but something functional. To make things clear, people who just want to play with the code can make it yours by cloning, forking, or downloading a copy of it from the <a href="https://github.com/fharper/HTML5challenges001-canvas_fileapi" target="_blank" rel="noopener noreferrer">repository on GitHub</a>. For others, I'll explain each part, and if you have any questions, please let me know in the comment section.

For the rest of the post, to save some space, I assume you know the basics of HTML, so I will paste or write only about things directly related to the challenge (example: I won't paste the import statement for my own JavaScript file), but the sources on my <a href="https://github.com/fharper" target="_blank" rel="noopener noreferrer">GitHub profile</a> are complete. Note also that all my code has been verified with the <a href="https://validator.w3.org/" target="_blank" rel="noopener noreferrer">HTML W3c </a><a href="https://validator.w3.org/" target="_blank" rel="noopener noreferrer">validator</a>, <a href="https://jigsaw.w3.org/css-validator/" target="_blank" rel="noopener noreferrer">CSS W3C </a><a href="https://jigsaw.w3.org/css-validator/" target="_blank" rel="noopener noreferrer">validator</a>, and <a href="https://www.jslint.com/" target="_blank" rel="noopener noreferrer">JSLint</a> (note that for JSLint you'll never have a perfect validation with my code as I ignore some of the errors it's reporting). I also make the code, and tested in on the latest releases (no nightly builds) of Internet Explorer, Firefox, Chrome, Safari, and Opera.

Let's start with the HTML code:

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-htmlchallenge-html

The <em>&lt;input&gt;</em> of type file will give us the opportunity to open the image to draw on it. We won't use a form here to load the file as we'll use File API later. The <em>&lt;button&gt;</em> element will give us the opportunity to take the draw on the <em>&lt;canvas&gt;</em> element, and fire up some JavaScript code that will create the image we'll be able to save. For now, it is disable as we didn't load an image yet, so this button is useless. The <em>&lt;canvas&gt;</em> element will let the user draw on the image we'll load. Last but not least, the <em>&lt;img&gt;</em> element where we will load the result of our saved image so users will be able to load it. Nothing very exciting there, but you have the first step to a successful challenge. Now, let's take a look at where all the magic happens, the JavaScript file:

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-1-js

The first thing is to prepare our application to react to different events. Right before, we'll check if the browser supports <em>canvas</em> by using a subset of Modernizr, and if the browser support also the<em> File API</em>. If it's the case, let's add a simple change event on the file input so we'll be able to load the file when the user will select one. We'll add <em>mouseup</em>, and <em>mousedown </em>events to the <em>canvas</em> so we know when the user will draw on it. Last but not least, we'll add a <em>click</em> event to the generate button to fire up the function that will save the image from the <em>canvas</em>. If the browser use by the user don't support <em>canvas</em> or <em>File API</em> will disable elements on the page, and let him know about the fact he can't use our application. The second part of the code is the function that will load the file loaded by the user into the <em>canva</em><em>s</em> element.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-2-js

The first thing to do is to make sure that the <em>canvas</em> element is visible, and the <em>img</em> is not. It's not critical, but I added these lines of code to make sure the users can use the tool more than once without having to refresh the page. The magic happens at line 9, where I started to access the file with the <em>FileReader</em>, and I'll start to read it with the <em>readAsDataURL</em>. After this, I'm setting an event handler once the operation will be successfully completed. In that case, I want to load the image that I accessed with the input field of type file. Once the image is loaded, I'll resize the <em>canvas</em> element with the size of the image the user selected, so it will work with any image size as little or as large they will be. I'll do the same with the hidden <em>img</em> element that I'll use later to create the modified image. Last, but not least, because the <em>canvas</em> itself have no drawing abilities, we need to get one of his context, in our case, the 2d one, and use some script to do it. By using <em>getContext</em> on the <em>canvas</em> I'm able to draw on it, like drawing the image I built a couple lines before.

Now, I need to let the user draw on the <em>canvas</em> so I defined the <em>startDrawOnCanvas</em> function that I used in the first JavaScript code of this post.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-3-js

There is nothing complicated here: I'm setting a listener on <em>mousemove</em> on the <em>canvas</em> element, so if the user moves his mouse over the <em>canvas</em> when the mouse was down (remember the listener I added at the beginning), the function <em>drawOnCanvas</em> will be fired up. I did the same thing to stop the drawing by removing the same listener when the mouse is up.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-4-js

Now, let's check one of the <em>biggest</em> function, or I should say, one of the most important one for this challenge, the drawing function.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-5-js

Actually, it seems worse than it is. Firstly, let's get some data to draw on the <em>canvas</em>. We need to access the left, and top from the canvas, since the position of the mouse will be relative to the left top corner of the browser window. Once we have those positions, we can start to draw by, of course, getting the 2d context again. In my code, I used the <em>fillStyle </em>function to set the colour to black, but it's just for this challenge purpose, as the default colour is already black.

The fun begins with the <em>beginPath</em> function. I would have been able to use something simpler like <em>fillRect</em>, but I figured out that if we are going to have only one tool to draw, a circle would be better. To create a circle, we need to create a path by starting it with the begin function, and closing it with the close one. Everything between those two functions will make our path, in that case, an <em>arc</em>. The function takes 5 parameters: the x coordinate where we will start the drawing, the y coordinate where we will start the drawing, the radius of the circle (5 is totally arbitrary, I thought the size was good enough for drawing), the starting angle (in radians - we'll start at 0), and the end angle (also in radians - Math. PI *2 will make a full circle). In theory, you can also add a last optional parameter to tell the function to draw counter-clockwise, but it changed nothing in our case. At the end, we are calling the <em>fill</em> function to render the path we just created.

The last JavaScript function is the one I used to create the <em>img</em> the user will be able to save.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-6-js

In that case, the only important lines are 6, and 7. We are setting the <em>src</em> of our hidden <em>img</em> by creating an image from the <em>canvas</em> element using the <em>toDataUrl</em> function. After this, the user will be able to right-click where he was drawing, and save the file. Another solution would have been to use a trick with <em>window.location.href</em> (see the code below), but it's not implemented in all browsers yet.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-7-js

For this not so beautiful HTML page, I used very little CSS.

https://gist.github.com/fharper/213a9b876a3ede3525fa9ee63e01a9a7#file-1-css

Let's start with the <em>#image</em> one. I'm telling the browser to hide the element when it's loaded, and set to an absolute position at 0 pixels from the left. It will give me the opportunity to have the image the user will save, and the canvas element one over the other, so when the user will ask to save the image, he won't have to deal with an element elsewhere in the page. Not critical, but I thought it would give a better experience. As for the rest, nothing complicated here. Oh, maybe you didn't see a lot of attribute selector, like the <em>[disabled]</em> I used with <em>#imgSave</em>. It just means that if this element have this attribute, this CSS will be rendered.

That's it, you now have a simple HTML page that lets the users load an image, draw on it, and save the new masterpiece to his computer. <strong>So did you do the challenge? If you did, please share your result with us in the comment section. Did you had any problem? Do you find anything that I can improve? Do you have any challenge you would like to see? Did you find this one useful? Share your thoughts, and keep looking at my site for the next one.</strong>

P.-S.: It's a pain in the ass to find a good code plugin for Wordpress, so hope you'll like the one I choose. I replaced the one I had, as this one is better, and it's the less worse I found!

Creative Commons: https://www.w3.org/html/logo/