---
ID: 2821
post_title: 'Ginger &#038; WYSIWYG, not playing well together'
post_name: ginger-wysiwyg-not-playing-well-together
author: Frédéric Harper
post_date: 2013-08-01 14:30:41
layout: post
link: >
  https://fred.dev/ginger-wysiwyg-not-playing-well-together/
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
<figure><img alt="2013-08-01_0953" src="http://fred.dev/wp-content/uploads/2013/08/2013-08-01_0953.png" width="501" height="415"/></figure><p>If you are using <a href="https://www.gingersoftware.com" target="_blank" rel="noopener noreferrer">Ginger</a>, the grammar corrector, with a WYSIWYG (What You See Is What You Get) editor, like the one in Wordpress, be aware that Ginger may add spaghetti to your code. I'm trusting TinyMCE inside of Wordpress for years as the code it generates is valid, and is far better than it was before, but one week ago I noticed something in my code: Ginger was adding HTML elements to it, his way to manage the correction in my text. What a surprise to see that sometimes, this code was saved in my post. The result? An HTML code stuffed of span that shouldn't be there after I finished the correction. Here is an example:</p><p style="padding-left:30px">More concretely, it means going to conferences, user groups, startup incubators, universities…. <strong>&lt;span class="GINGER_SOFATWARE_correct"&gt;</strong>to<strong>&lt;/span&gt;</strong> present about your technology, to talk with, and meet people. This is where you will build strong relationships, and where you'll find <strong>&lt;span class="GINGER_SOFATWARE_correct"&gt;</strong>influencers<strong>&lt;/span&gt;</strong> to help you achieve your goal, and scale. It's not just about conferences, think about <strong>&lt;span class="GINGER_SOFATWARE_noSuggestion GINGER_SOFATWARE_correct"&gt;</strong>hackathons<strong>&lt;/span&gt;</strong>, and workshops: they are good places to help people learn your API, or start to use your product. You can also leverage what you are doing offline, online, by doing video interviews, recording your talk or doing recapitulation blog posts.</p><p>Maybe it was a bug for a specific version, perhaps it was a problem with Wordpress, but it was enough to remove Ginger, and clean my code (I still need to look in older posts to see if there is still improper code). At the end, I don't want any plugin or application to miss with the code from my posts. If Ginger screw your code too, use an editor like <a href="https://www.sublimetext.com/" target="_blank" rel="noopener noreferrer">Sublime Text</a> who can find &amp; replace with regular expression, and use the number 1 to find, and number 2 to replace:</p><ol><li>    (GINGER([^&lt;]*))&lt;/span&gt;</li><li>    1</li></ol><p>It will find all the <em>&lt;/span&gt;</em>, and replace them with everything in the first parenthesis (the code/text we want to keep for now). After this one, we can now remove the first part of the Ginger &lt;span&gt; by using the next string to find, and replace it with nothing:</p><ol><li>    &lt;span class="GINGER([^&gt;]*)&gt;</li></ol><p>It should leave you with a clean code, at least without any Ginger specific elements. I tried it on many posts with success. Hope it will help you too.</p><em>P.S.: I wonder if the class GINGER_SOFATWARE is a typo by developers or not.</em>