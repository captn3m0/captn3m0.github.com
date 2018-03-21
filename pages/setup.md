---
title: The Setup
permalink: /setup/
layout: page
image: spectrum/poster.jpg
video: spectrum_320.mp4
image_alt: "Music Visualization Demo"
---

## Who am I, and what do I do?

I'm Abhay Rana, more popularly known as Nemo. I am a hacker, web developer, writer,
and a UX enthusiast. ~~I am working on a book called [The Joy of Software Development][josd].~~

I do tech and security related things at [Razorpay](https://razorpay.com).

## What hardware do I use?

![My current work setup](/img/ama_setup.jpg)

Most of my work is done on my Macbook Air 2015 running Arch Linux.

My phone these days is a [Moto Z Play][moto] (running [Lineage OS for MicroG][ug]). I backup all of my media to my home server. Other than this, I own a Kindle Paperwhite and an iPad 2 (which I exclusively use for reading books and comics). For my music, I have a pair of [Sennheiser HD 202][hd-202], an excellent pair of headphones considering the price. 

I am an ocassional gamer and use the [Logitech G300s][g300s] for both gaming and productivity (its heavily customizable). Since my laptop speakers aren't exactly top-notch, I rely on my [Logitech X100][x100] bluetooth speakers for listening in closed spaces.

I own a [Leopold FC660C][fc660c] keyboard (Topre switches) which I use at work. My backup keyboard at home is a [Cooler Master QuickFire Rapid-i][quickfire] mechanical keyboard (Cherry MX brown).

At home, I have a Raspberry Pi 2 Model B and a PC/HomeServer, which runs lots of tiny services, which are proxied over to the internet with a Digital Ocean droplet in the `BLR1` region. I wrote about it in [detail][homeserver].

I am also a speedcuber; my primary cube is a [QiYi Thunderclap][thunderclap] (stickerless). I also own several
other twisty puzzles, including a Mirror Cube and a Megaminx.

## And what software?

(audio warning)

<video 
    src = "/videos/spectrum_320.webm"
    width = "100%"
    poster = "/img/spectrum/poster.jpg"
    onclick = "this.paused?this.play():this.pause();"
    title = "Spectrum Visualization Demo."
    class = "center-content"
></video>

My current distro is [Arch Linux][arch] with [i3][i3] as the window manager. My most used tools include: [Neovim][neovim], [Sublime Text 3][sublime], Firefox Beta, and Git. I game using Steam, and purchase DRM free games via Humble Bundle whenever possible. The above animated wallpaper runs via [spectrumyzer][wallpaper-blog].

Most of my work is done in editors, command line, and the browser. A few essential extensions on my browser include: [dotjs][.js] (with apache support), [Privacy Badger][privacybadger], [uBlock Origin][ublock], HTTPS Everywhere, LastPass, and Markdown Here.

I am a [Hacker News][hn] addict, and have even [written an application][hackertray] for it. Most used webapps would be: Slack, GitHub. I use AirSonics for listening to music on the go, and `cmus` on the desktop.

I run lots of tiny services on my homeserver, including [Gitea][gitea], OpenVPN, Emby, and Grafana. I have my Kindle jailbroken and run [KOReader][koreader] to read EPUB files and PDFs with reflow (seriously, it is better than sliced bread).

## What would be my dream setup?

A lightweight laptop with tons of battery life, 13" display, and official Linux support (Dell XPS13 DE comes close).

If we're talking super-crazy, I'd love to have a thought-dictation feature. That would help _a lot_ with my writing.

[galago]: https://system76.com/laptops/galago
[moto]: https://www.motorola.com/us/products/moto-z-play
[hd-202]: http://en-us.sennheiser.com/over-ear-headphones-hd-202
[g300s]: http://support.logitech.com/en_us/product/g300s-gaming-mouse "Lots of buttons, which I use for my window manager"
[x100]: https://secure.logitech.com/en-hk/product/x100-mobile-wireless-speaker "Its not very loud, but very good for indoor use"
[quickfire]: http://gaming.coolermaster.com/en/products/keyboards/rapid-i/ "The backlighting on this keyboard is insanely customizable"
[thunderclap]: http://www.speedcubereview.com/qiyi-thunderclap.html "No backup cubes at present"
[arch]: https://www.archlinux.org/ "Rolling, lightweight distro for Linux"
[i3]: http://i3wm.org/ "i3 is a tiling window manager"
[neovim]: http://neovim.io/ "Fork of vim for modern platforms"
[sublime]: https://sublimetext.com/3
[hnapp]: http://aws-hn.premii.com/about/ "Supported on web, iOS and Android platforms"
[adaway]: https://sufficientlysecure.org/index.php/adaway/ "Blocks ads on android devices using host files"
[afwall]: https://github.com/ukanth/afwall "AFWall is a firewall for Android"
[ublock]: https://github.com/gorhill/uBlock/ "uBlock Origin"
[privacybadger]: https://www.eff.org/privacybadger "Privacy Badger (by EFF) blocks spying ads and invisible trackers"
[hn]: https://news.ycombinator.com "Hacker News"
[josd]: https://josd.captnemo.in/ "Joy of Software Development, Book I'm working on"
[pirunner]: https://github.captnemo.in/pirunner
[.js]: https://github.captnemo.in/dotjs "This is my fork of the original dotjs that runs on top of local Apache with a working SSL Certificate"
[libreelec]: https://libreelec.tv
[hackertray]: https://github.captnemo.in/hackertray "HackerTray is a app-indicator based status menu app for Hacker News (linux)"
[koreader]: https://github.com/koreader/koreader "Document reader for Kindles that has EPUB and PDF Reflow support"
[wallpaper-blog]: "/blog/2017/05/01/spectrumyzer-visualization/" "I wrote a blog post about how I made my animated wallpaper"
[fc660c]: https://deskthority.net/wiki/Leopold_FC660C "I haven't typed enough on it yet to have an opinion"
[ug]: https://lineage.microg.org/ "Access all the Google services without proprietary closed software"
[homeserver]: https://captnemo.in/blog/2017/09/17/home-server-build/
[gitea]: https://git.captnemo.in