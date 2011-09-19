---
title: Six Months of Ubuntu
layout: post
tags: ubuntu, operating systems, weblog-ifest
---

I installed Ubuntu as my primary OS back sometime in February. Not that I'd not tried it earlier. In fact, I'd used a copy of Ubuntu 3 back in day. But this time around, Windows (from my dual boot) just gave up and died. The partition with Windows got heavily corrupted, lost lots of data, and ultimately I had to format it. And Ubuntu dragged through all that. And here I'm today, a veteran of 3 Ubuntu versions, starting with 10.10, and right now on the 11.10 beta. 

What have I learned ? That its better than Windows, for one. But several other things as well. I'm writing this post from the general linux-distro scene, and not just Ubuntu in specific. For the period before Feb, I'd been using Linux Mint as my primary OS for quite some time. But Ubuntu Natty Alpha brought all that Unity love (which I doted on once), and I had to move to 11.04

##Reasons to switch to Linux
1. Its free!
2. Its free! No more paying up for Windows. People who had Windows ship with their computers would be delighted to know that there is something called a Windows Refund, which allows you to be compensated by the cost of Windows, if you decide not to use it.
3. Better file system. If you've ever lost yourself in the mirth of files in "Program Files", "AppData", "Application Data", "sytem32" and the like, you'd be delighted to know that there is a very well balanced binary management system in Linux. All binaries are in PATH, unlike Windows, where some softwares do that, and most don't. So you can actually run `php`, `git`, `ruby` from any damn place that you want. People who have tried to compile Java programs using `javac` on Windows might remembring updating PATH in Windows. No more of that in Linux.
4. Free softwares! The majority of good software on Windows is paid (and even more with Mac). But in the Linux world, (almost) everything is free. What is paid for then? Some games, high level commercial softwares and the like. But most of the stuff is free.
5. **Package Management** Apparently Windows 8 will have some sort of app-store with it. Which is a long time coming in Windows. But guess what, almost all Linux distros have some flavor of package manager built in. Debian (and Ubuntu) has `apt-get`, Arch has `pacman`, Fedora has `yum`. And installing softwares is as easy as it could be. Need mysql? Just type `sudo apt-get install mysql`. Done. Boom. Just like that.
6. **Customization Level** Even though I don't like the messing up of Gnome by Ubuntu, there are tons of alternatives available. I'm right now using Gnome-Shell, and have plans to move to `xmonad`, which is another Window Manager. Almost every feature on the Linux desktop can be customized. 
7. **Terminal** I'd always had planned several `learn bash scripting` kind of to-dos but never got to it until I started using Linux. Even if you don't script, the actual power of your machine is opened by the terminal. Hacking away in `vim`, and browsing sites using `elinks`, and ordering Pizzas in Command Line is as geeky as it gets. Gnome is designed in such a way to allow a normal user to use his computer fully without touching the terminal, but if you use it, it gets better &amp; better.
8. **Applications** There was a time I used to be a Windows fanatic, using WMP, Zune, Everything and what not. But now, I've got a bigger arsenal of softwares. Ever used *Audacious*? That's my default music player, and its awesome.
9. **Software Development** You use Windows to develop stuff for Windows. I'm nowhere near to writing applications in C#. I'll probably be hacking away scripts in ruby, node, python, bash, and building stuff using xul, gtk, webgtk, and qt. All my web applications are ultimately deployed on Linux machines, so it makes sense to write them on Linux. And only Linux has the ease of language package managers, like rubygems, npm, and pip. 
10. **Open Source** I haven't yet checked out the Linux Kernel source code, but I'm thinking of getting my hands dirty real soon. Ever since I've joined github, I've been introduced to several awesome coders, projects, and organizations. And guess what? Its all open source! Meaning I actually spend less time writing parsers for xml, and more time working on applications.

##What I've Learned
1. **Be utterly fearless** Back when I was in Windows, a simple partition deletion used to scare me to death. Now? I'm ready for anything. If you, like me, go play with the alpha of all your favorite stuff, then things will break. And it will be fun to solve all that stuff. You will learn a thousand new things in the process, gain lots of rep on askubuntu, and become a Ubuntu Jedi Master. OK, maybe not the last bit, but *you shall become utterly fearless* of all danger. I had to use my computer without network accesibility for three days. And it didn't even give me a GUI. So I just drudged along for 3 days straight on the console. :)
2. **Community** Sometimes, I feel people do not get my helpful comments, and offerings of help on Facebook. Its not their fault. They've never been introduced to a proper online, helpful community before. The Linux community is helpful, worldwide, readily available, and has probably handled the problem that you are facing now.
3. **Server Administration** I'm still lacking on the cloud front, as I don't have servers powerful enough to host virtual machines. But otherwise, I've handled lots of stuff. `ssh` is my thing, and I use `git` to deploy applications like a pro. I've moved on from `apache` to `nginx` to `cherokee` and what not.
4. **Take Backups** Remember all those "Take Backups before installing Windows/Ubuntu" things that popup while installing your OS. I never paid attention to them, until recently. Now, I've got backups scheduled on `Dropbox`, `SpiderOak`, and a custom `SparkleShare` server. I make sure to host my code on github, or my personal git repositories and backup images to Picasa. Everyone knows hard discs are unreliable, so why not make your data redundant and take backups.

The only counter argument would be that Windows has much more stream-lined view of things, with almost everything offering a GUI based application to amange stuff. That's just not the Linux way. Still, I'm not one of those crazy fanatics who go around preaching Linux (maybe I am!). I feel that if you are using your computer to just open Chrome, Firefox, VLC, and Word, then anything would do. You could probably install android on your computer and do everything you are doing right now. If you are a heavy gamer, then better stay with Windows. And if you are a programmer, switch to Linux.

##Windows 8
I installed a developer preview copy of Windows 8 recently, and although I was really awed by its designs concepts, I feel that it is still lacking in certain fronts. For instance, it seems to me that Microsoft is trying to get 8 to the tablets much more readily than on the desktops. Why? Because, there is nothing that can undermine Windows superior market share in Desktops for the near future. However Android & iOS have a very strong presence. Ergo, Windows 8 goes to tables. 

I installed all my favorite programs on Windows 8, but had to switch back after a few days. As a developer, it just does not offer me the same freedom, and easy workflow that I am accustomed to. For instance :

* Installing Ruby with build support for gems took a lot of time and patience.
* Cygwin does not compare anywhere near to a bash shell. Its like this tiny humble brother of shell who turns away when you say PATH. You have to type all those monstrous `C:/\` kind of paths.
* No App Store. Windows 8 dev preview does not have an app store yet, which was one of the reasons I had tried Win8. I'm used to frequently browsing the Ubuntu Software Center just to find something that fits.
* I found that my productivity reduced to half when I was on Windows. I spent too much time looking for stuff which could be done by a single line bash on Linux

Tags: operating systems, linux, ubuntu, windows 8, weblog ifest 2011
