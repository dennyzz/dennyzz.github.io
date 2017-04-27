---
layout: post
title: Github Pages Website
description: a Github Pages Website powered by Jekyll
imgroot: /images/projects/github.io
img: /cover.jpg
---

This website will be project #1 to fill in things as I go 

This will be another foray into the web development that I find as somewhat fun. Learning how to use code to make a certain visual aesthetic is rewarding. With all these new web development tools, standards, and applications, there's just so much choice behind what kind of website to go with. There's a Wordpress blog, which I found a bunch of themes which I would have paid for, except free Wordpress hosting does not allow outside themes. I could have grabbed a free Amazon EC2 server and made my own hosting environment. From there I would have to figure out what languages I wanted to use, whether a LAMP stack of a XAMP stack or something, and then basically start from scratch in making some kind of website. It would only cost me a few bucks a month to run, and maybe having that money go into it would help motivate me, but it still looks like too much work if I only want to worry about content. I was unable to find a free wordpress theme that I wanted to use that would let me do hosting a blog style side for the occassional thought, and then a blog style documentation of any projects of mine, while also having support for a photo gallery with which to upload the albums fulls of pictures that I take with my camera. So here we are with Jekyll. It's free, and has enough freedom to let me make this website as I please, while also having enough theming and simplicity to do much less work. Did i mention that it's free? I just need to find a better github name since DennyZhang and DennyZ are both taken.	

So we're starting with this <a href="https://github.com/bogoli/-folio">*folio</a> theme which I thought looked pretty good. Now since I am running on a windows machine it is much more painful to set up Jekyll on the OS, so we'll just let Github take care of all the compilation.

Now as Dropbox has ended support for the "Public" folder, we can moved all of our assets to hosting on AWS. This should be relatively cheap, since this site does not drive that much traffic anyways and is not meant to. There should be no noticeable difference except maybe things will load slightly faster.