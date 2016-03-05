---
layout: post
title: New Design of CaptNemo.in
tags:
- design
- captnemo.in
---

I did a redesign of the blog. The main goals for the redesign were to reach a 
clean, readable layout, which I feel I've accomplished.

### Pics
<iframe frameborder='0' height='540' width='100%' src='http://min.us/mbneXkYyXF/3e'></iframe>

### Old Design
Everything was plain old bootstrap, except for the hover effect on the 
photograph. I've also removed the old "Related Posts" feature, which I felt was 
not at all useful. In the old homepage, the list of articles was earlier presented as a list (\<li\>), while it is now slightly better. The topbar has also been removed, instead focussing on a far better sidebar.

### New Stuff
I wanted a _clean design_ more than anything. So instead of the sharebox being persistent on every device, I decided to hide it on lower resolutions. It currently hides if the screen width < 1100px, so unless you are on a widescreen resolution monitor and using your browser on fullscreen, you won't see it.

Responsive design via bootstrap allows you to easily support mobile devices. The left sidebar is stacked, so that even mobile devices have no problem with the layout.

I'd describe the design as _clean, minimal_. 

### Bootstrap
The earlier design was using Bootstrap 1.3, and I've upgraded to 2.0.2 now. 
I've used the new version before, but with zero changes using 
[bootswatch](http://bootswatch.com/) in [a few other places](/codechef/). But 
this time, I decided to tweak bootstrap for my needs.

I did away with the navigation bar, and changed the default fonts. The site 
does not feel like a stock bootstrap site any longer. The major contribution 
from bootstrap, was in fact the grid system, and the responsiveness, which 
really helped me get it done quickly.

### Typography
The fonts used are [Ubuntu](http://www.google.com/webfonts/specimen/Ubuntu) for the content, and [Gentium Book 
Basic](http://www.google.com/webfonts/specimen/Gentium+Book+Basic) for the 
headings. I'm using [Google Web Fonts 
Directory](http://www.google.com/webfonts) for the fonts.

I'm only loading the italicized version of Gentium as I've chosen to display 
all headings (h1-h6) as italics. 
