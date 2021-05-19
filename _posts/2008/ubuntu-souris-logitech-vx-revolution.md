---
ID: 3210
post_title: 'Ubuntu &#8211; Souris Logitech VX Revolution'
post_name: ubuntu-souris-logitech-vx-revolution
author: Frédéric Harper
post_date: 2008-06-07 17:33:41
layout: post
link: >
  https://fred.dev/ubuntu-souris-logitech-vx-revolution/
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
<div id="deadblog">
  Ce billet a été initialement rédigé sur le défunt blogue À la base 2
</div><img style="float:right" title="Ubuntu" src="http://fred.dev/wp-content/uploads/2008/06/ubuntu-logo-290x300.png" alt="Ubuntu" width="150" height="155"/ Bien sû r un blogue c' est une porte ouverte sur le monde cyberné tique, maisç a ne se limite pasà ç a. En fin de compte, un blogue, c' est tout ce qu' on veut queç a soit. Aussi simple queç a. Pour moi, ce blogue se redé finit au fur età mesure de mon utilisation. En plus d'ê tre une vitrine pour donner mon opinion sur certains sujets, je vais aussi m' en servir comme un bloc-note. J' ajouterais ici des billets de type plus technique, question de garder une trace sur des problè mes que j' ai confronté s au niveau professionnel et personnel. De plus, cela permettra de transmettre cette information. Vous verrez aussi certaines fois, un peu comme pour ce billet, ou je ré pé terais les informations que j' ai trouvé es utiles. Selon moi, plus il y a de sources qui pré sente la mê me information, plus celle-ci me semble cré dible. Puis pour terminer, j' ajouterais aussi surement certains billets ou je traduirais de l' information trouvé e en anglais, car certaines fois on manque de ressources francophones!< p/>Venons-en au coeur du billet. Je suis revenu sous Linux il y a peu de temps, alors quand j'ai un peu de temps pour relaxer, j'essaie d'améliorer mon expérience. J'ai donc voulu rendre fonctionnels les multiples boutons de 

[ma souris][1]. [Ubuntu][2] a plusieurs tutoriels très bien faits, mais celui concernant ma [Logitech VX Revolution][3] me semble un peu éparpillé. Je ne sais pas si c'est moi qui n'a pas bien compris, car il est vrai que j'étais habitué aux tutoriels de [Gentoo][4] (ayant été sous Gentoo pendant 3-4 ans avant).
Bref, voici les étapes que j'ai dû faire pour réussir le tout.

On doit tout d'abord aller prendre en note le chemin de notre souris en tapant le code suivant :

<pre lang="bash">find /dev/input/by-id/ -name "*event-mouse"</pre>

Cela devrait vous retourner quelque chose du genre :

<pre lang="bash">/dev/input/by-id/usb-0d3d_USBPS2-event-mouse
/dev/input/by-id/usb-Logitech_USB_Receiver-event-mouse</pre>À ce point, prenez en note celle qui contient le mot "Logitech" dedans.

Pour pouvoir gérer les touches et leurs associés des actions, vous allez avoir besoin de deux logiciels, soit [XBindKeys][5] pour associer un bouton a une action et [Xvkbd][6] pour associer des touches ou combinaison de touches a une action. Pour ce faire, tapez cette commande :

<pre lang="bash">sudo apt-get install xserver-xorg-input-evdev xbindkeys xvkbd</pre>

Vous allez devoir modifier les configurations de Xorg, alors pour des questions de sécurités, faites une sauvegarde de votre fichier xorg.conf:

<pre lang="bash">sudo cp /etc/X11/xorg.conf /etc/X11/xorg.conf.backup</pre>

Ensuite, éditons ce fichier :

<pre lang="bash">sudo gedit /etc/X11/xorg.conf</pre>

C'est un peu à partir d'ici que je trouve qu'ils se sont compliqué la vie. Dans mon cas, la partie de ma souris dans mon xorg.conf ressemblait à ça :

<pre lang="bash">Section "InputDevice"

<p>
  Identifier      "Configured Mouse"
</p>




<p>
  Driver          "mouse"
</p>




<p>
  Option          "CorePointer"
</p>




<p>
  EndSection
</p></pre>

Modifiez la ligne "Driver" et remplacée la par ça :

<pre lang="bash">Driver          "evdev"</pre>

Ensuite, à la suite de la ligne "Option", ajoutez ce code :

<pre lang="bash">Option          "Device" "/dev/input/by-id/usb-Logitech_USB_Receiver-event-mouse"

<p>
  Option          "Protocol" "ExplorerPS/2"
</p>




<p>
  Option          "Emulate3Buttons" "false"
</p>




<p>
  Option          "Buttons" "11"
</p>




<p>
  Option          "ButtonMapping" "1 2 3 9 8 6 7 13 14"
</p>




<p>
  Option          "ZAxisMapping" "4 5"
</p></pre>

Où vous remplacez le "/dev/input/by-id/usb-Logitech_USB_Receiver-event-mouse" par celui que vous avez trouvé plutôt.

Ce qui vous donnera pour votre souris, quelque chose de semblable :

<pre lang="bash">Section "InputDevice"

<p>
  Identifier      "Configured Mouse"
</p>




<p>
  Driver          "evdev"
</p>




<p>
  Option          "CorePointer"
</p>




<p>
  Option          "Device" "/dev/input/by-id/usb-Logitech_USB_Receiver-event-mouse"
</p>




<p>
  Option          "Protocol" "ExplorerPS/2"
</p>




<p>
  Option          "Emulate3Buttons" "false"
</p>




<p>
  Option          "Buttons" "11"
</p>




<p>
  Option          "ButtonMapping" "1 2 3 9 8 6 7 13 14"
</p>




<p>
  Option          "ZAxisMapping" "4 5"
</p>




<p>
  EndSection
</p></pre>

Il ne vous reste plus qu'à ajouter une ligne dans la section "ServerLayout":

<pre lang="bash">InputDevice     "Configured mouse" "SendCoreEvents"</pre>

Ce qui me donnait dans mon cas, un "ServerLayout" comme suit :

<pre lang="bash">Section "ServerLayout"

<p>
  Identifier      "Default Layout"
</p>




<p>
  Screen          "Default Screen"
</p>




<p>
  InputDevice     "Synaptics Touchpad"
</p>




<p>
  InputDevice     "Configured mouse" "SendCoreEvents"
</p>




<p>
  EndSection
</p></pre>

Bien sûr, vous pouvez modifier le nom donné par défaut "Configured Mouse" comme vous voulez (exemple: "Logitech VX Revolution"), mais vous devez vous assurer que vous utilisé le même nom dans les deux sections.

Rendu à ce point, sauvegardez votre fichier de configuration et redémarrez GDM (ou KDM si vous utilisez KDE):

<pre lang="bash">sudo /etc/init.d/gdm restart</pre>

Si tout va bien, X va repartir et votre souris fonctionnera encore. Dans le cas contraire, remettez votre configuration initiale et tentez de trouver pourquoi!

Maintenant que votre souris fonctionne, voyons voir comment assigner des actions à vos touches.

Il vous suffit de créer un fichier .xbindkeysrc dans votre home :

<pre lang="bash">gedit .xbindkeysrc</pre>

Puis ajoutez les actions ici. Voici ce que donne mon fichier de configuration :

<pre lang="bash"># molette vers la droite -&gt; rien encore
#
#m:0x0 + b:6

# molette vers la gauche -&gt; rien encore
#
#m:0x0 + b:7

# zoom + -&gt; augmentez le volume de 5%
"aumix -v +10"

<p>
  m:0x0 + b:13
</p>

# zoom - -&gt; diminuez le volume de 5%
"aumix -v -10"



<p>
  m:0x0 + b:14
</p>

# Bouton latéral bas -&gt; page suivante dans firefox
"/usr/bin/xvkbd -xsendevent -text "[Alt_L][Left]""



<p>
  m:0x0 + b:8
</p>

# Bouton latéral haut -&gt; page précédente dans firefox
"/usr/bin/xvkbd -xsendevent -text "[Alt_L][Right]""



<p>
  m:0x0 + b:9
</p>

# bouton loupe -&gt; Ouvrir firefox
"firefox"



<p>
  m:0xO + c:99
</p></pre>

Donc, la syntaxe est de mettre la commande en premier et ensuite mettre le bouton utilisé. Une fois configurez, lancez XBindKeys:

<pre lang="bash">xbindkeys</pre>

Comme vous voulez que ça fonctionne chaque fois que vous vous connectez a votre compte sous Gnome, ajoutez cette application dans "Système -> Préférences -> Sessions" sous l'onglet "Programmes au démarrage".

Voilà!

Dans mon cas, j'utilisais Ubuntu 8.04 (Hardy Heron) pour faire ces modifications. En espérant que cela vous a aidé (même si c'est simplement pour clarifier le tutoriel sur Ubuntu), mais dans tous les cas, ça me fait une trace si je dois réinstaller Ubuntu éventuellement.

<p style="text-align:center">
  __________
</p>

<p style="text-align:center">
  <span style="font-size:xx-small"><em>Source de l'image: <a title="Source de l'image" href="https://theconsumerscorner.net/">The Consumer's Corner</a></em></span>
</p>

 [1]: https://www.logitech.com/index.cfm/mice_pointers/mice/devices/165&cl=ca,fr "Site web de la souris Logitech VX Revolution"
 [2]: https://www.ubuntu-fr.org/ "Site web de Ubuntu"
 [3]: https://doc.ubuntu-fr.org/souris_logitech_vx_revolution "Tutoriel de Ubuntu sur la Logictech VX Revolution"
 [4]: https://www.gentoo.org/ "Site web de Gentoo"
 [5]: https://hocwp.free.fr/xbindkeys/xbindkeys.fr.html "Site web de XBindKeys"
 [6]: https://homepage3.nifty.com/tsato/xvkbd/ "Site web de Xvkbd"