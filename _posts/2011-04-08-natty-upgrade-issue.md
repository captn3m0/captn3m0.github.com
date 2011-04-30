---
layout: post
title: Issue with natty upgrades
---
I upgraded to Natty narwhal recently from Maverick, and used the CD based installer. It gave me an option for upgrading to Natty from Maverick, but I did not read the fine print that asked me to backup everything first. I thought, hey, it isn't going to delete my home directory, so why should I be worried. But as it turned out using a sudo apt-get upgrade -d is much better than the CD installer. The CD decided to remove all of my programs, everything under /var, and several other places as well. Unfortunately I did not pay heed to the warnings, and was shocked to see my /var/www folder missing after the install. Even though I had backups, there are a few things still missing.

So, all is well with ubuquity, but next time Oneric Oncelot comes around, I will stick with `sudo apt-get upgrade -d`.  
