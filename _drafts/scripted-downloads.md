---
layout: post
title: Faster downloads from file sharing sites
---

I have worked previously with [RapidLeech][rl] before for downloading files off a file-sharing site, mostly because it is based in PHP and allowed me to write a faster version of its mediafire downloader, which was once hosted at mfroaster.co.cc. However the problem with such downloading scripts is that they rely on web page parsing to detect various packing techniques that these sites employ. To circumvent this, Rapidleech uses modules for each of these sites, which tackle the difficulty of using regexes to calculate the final download link. There is a big shortfall to this issue and is related to the updating nature of these sites. Once they change their code, it goes down.

I had earlier tried to take a look at [Plowshare][ps] which is a Bash based file downloader for file-sharing sites. It uses [rhino][r] to parse the sites javascript, and downloads files automatically. The parsing part is handed over to Rhino and as such, it needs much less updation. But the issue with plowshare was it uses curl by default to download files. The latest version of plowshare, however supports external download tools as well (such as axel). 

Here are the scripts that I use

{% highlight bash %}
#! /bin/bash
plowdown   --run-download="axel -n 15 -a  %url" $1
{% endhighlight %}

Basically this downloads anything and passes the final download url to axel. The next issue cropped up with the google search. I wanted the number of steps to download a file to be bare minimum. When I search for something on google, the links to various pages are redirects via google. I looked around for some userscripts, but found none that worked (they were all from the pre instant-search era). What I wanted was something that gets activated at will and disables the redirects.

I personally use [dotjs][d] for my userscripts. It is as simple as dropping a file called google.com in your ~/.js folder for it to be automatically called at that url. The solution I came up with involved removing the Orkut link from the page top and transforming it to a Linkify link, which removes the redirects.

{% highlight javascript %}
$(document).ready(function() {
  $('.gb1').each(function(){
    if(this.innerHTML == 'Orkut'){
      $(this).mousedown(function(){
        $('.l').each(function(){
          $(this).unbind('mousedown');
          this.removeAttribute('onmousedown');
        });
      });
      $(this).html("Linkify");
      $(this).removeAttr("href");
    }
  });
});
{% endhighlight %}

To try it out install [dotjs][d] and save this file as google.com.js (or google.co.in.js) in your ~/.js directory. If your dotjs server is running, the Orkut link should be replaced by a Linkify one, which should remove the redirect.

Ultimately, I do this :
Search for file -> Click on linkify -> Copy link -> Paste on console. 

Have any doubts, let me know in the comments

[d]: http://defunkt.io/dotjs/
[r]: apt://rhino
[ps]: http://code.google.com/p/plowshare/
[rl]: http://rapidleech.googlecode.com/
