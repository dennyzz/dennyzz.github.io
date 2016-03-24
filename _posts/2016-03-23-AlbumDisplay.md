---
layout: post
title: Photo Albums Mosaic Style
date: 2016-03-23 22:30:00
description: Progress report 2 on building the photo albums section
---

More update on the photography section of the site. I'm set on this new display style for the photo albums. It uses xgallerify which is jquery and css to calculate and display the images in the fitted mosaic style. We had to change some fundamental css settings that were a part of the *folio theme, but everything else should still work as it has. 
The only problem we have with it is that the script doesn't run until all of the thumbnails have been loaded. This creates a small lag where the photos aren't the right shape and size before everything loads and it all snaps into place. 
I think this bug will stay for now, but it is noted, and when there is time to tweak it that will be a good idea to work with to start. 
I have uploaded a few more albums both to ensure that everything works and to check the speed for larger photo albums, and whether there is any noticeable lag scrolling through a large number of photos. 
The lightbox2 plugin still is still having some issues with creating the properly sized backing white border, but we'll leave it as I am in the process of looking for another lightbox/gallery plugin to do display once you click an image.
So, go on over and check it out [Here](/gallery/albums/cleland/)