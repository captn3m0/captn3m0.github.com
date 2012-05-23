---
title: How to run apt-add-repository behind firewalls (#iitr)
layout: post
tags:
- ubuntu
- snippet
---
Copied from [OMGUbuntu](http://www.omgubuntu.co.uk/2011/01/how-to-add-repositories-to-ubuntu-from-behind-a-firewall/)

1. Press Alt-F2 and type "gksu gedit /usr/lib/python2.6/dist-packages/softwareproperties/ppa.py"
2. Find line 88, change "keyserver.ubuntu.com" to "hkp://keyserver.ubuntu.com:80"
3. Save and close

Note that this is the default setting in Ubuntu Natty Narwhal (11.04), and was only applicable for Maverick or older versions.
