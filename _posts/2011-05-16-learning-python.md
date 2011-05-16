---
layout: post
title: Learning Python, PyGTK
---
I had been meaning to learn either Python or Ruby for a long time but had been unable to decide. I had a basic understanding of both of these, but I never had the chance to build an entire application in either. And I'm not talking about using [Django][django] or [Ruby on Rails][ror] (which are both brilliant), but building a desktop application using GTK.
The application I was first aiming for was a P2P sharing client which would be completely decentralized and offer several special features, such as :

* NAT Transversal using [UDP Hole Punching] [udp]
* HTTP based file sharing as well (so that people can install their clients, and __still use__ IDM for downloading stuff)
* Client discovery & routing behind firewalls along the lines of Skype ([using supernodes] [skype])

However my dreams were shattered by the first point itself, being the difficulty of NAT Transversals. Further ahead was the question of networking as well, which could have potentially driven me nuts. I worked a bit on it, using [STUN] [stun], [twisted] [twisted], but gave up on it soon as being unfeasable as a learning project. 

The next idea came to me when I got tired of downloading stuff using [axel] [axel] from the command line and started itching for something similar to [Internet Download Manger] [idm] for Ubuntu. The closest thing to a download manager on Ubuntu is [FatRat] [fatrat] and is something I really don't like. It is based on Qt and prouds on working as a front-end for several file-sharing websites as well. What I needed was in fact a fast download manager, which keeps tracks of what I download, and does not require keeping a terminal open all the time.

I found [GwGet] [gwget], which occassionaly looks much better in the source version than in the one from the Ubuntu Repositories. I really liked this one, except for the fact that it was made using C++, and used single threaded downloads (like wget). As a result it was quite slow, and not upto my needs. 

That was when I thought of the idea of creating a download manger using [GTK] [gtk] +  Python/Ruby. I looked around for axel ports in Python/Ruby and found [PyAxel] [pyaxel], which beat axel in some of my benchmarks (after [this patch] [pyaxelpatch]). For the past two days, I have been working on PyGTK, Glade, Anjuta and several other IDEs, none of them to my liking. I really prefer Vim :)

So far, the work on [PGet][pget] has been minimal. I've worked out threading, and little parts of GUI which were stripped from GwGet. As of now, it is still under works, but I am hoping for a release real soon. After all, it is not for nothing that they call Python a dynamic langugae


For more details, please go the [PGet] [pget] project page on Github. I will be posting further updates over there.
In case someone is following this blog, you can view the source for this website at [github](https://github.com/captn3m0/captn3m0.github.com 'This website on GitHub') and maybe even fork it!

[django]:	http://djangoproject.com 				"Django is a web framework for Python"
[ror]:		http://rubyonrails.org					"Ruby on Rails is a web framework for Ruby"
[udp]:		http://en.wikipedia.org/wiki/UDP_hole_punching
[skype]:	http://www.h-online.com/security/features/How-Skype-Co-get-round-firewalls-747197.html
[stun]:		http://en.wikipedia.org/wiki/STUN			"Stun is a NAT transversal server"
[twisted]:	http://twistedmatrix.com				"Twisted is a networking framework for Python"
[idm]:		http://internetdownloadmanager.com
[axel]:		http://axel.alioth.debian.org/				"Axel is a multithreaded download binary"
[fatrat]:	http://fatrat.dolezel.info/
[gwget]:	http://projects.gnome.org/gwget/
[pyaxel]:	http://code.google.com/p/pyaxel/			"Axel port to python"
[pyaxelpatch]:	http://code.google.com/p/pyaxel/issues/detail?id=4	"My patch for optimizing PyAxel's chunk size"
[pget]:		https://github.com/captn3m0/pget			"PGet home page on Github"



