---
title: The Setup
permalink: /setup/
layout: page
image: battlestation-shire.jpg
video: spectrum_320.mp4
image_alt: "Music Visualization Demo"
---

## Who am I, and what do I do?

I'm Abhay Rana, more popularly known as Nemo. I am a hacker, web developer, writer, and a UX enthusiast. ~~I am working on a book called [The Joy of Software Development][josd].~~

I do tech and security related things at [Razorpay](https://razorpay.com).

I run [HackerCouch](https://hackercouch.com/), which is like couchsurfing for hackers and [other projects](/projects/).

## What hardware do I use?

![My current home setup](/img/battlestation-shire.jpg)

Most of my work is done on my [Intel NUC (7th Gen, i7)][nuc]. My work laptop is a [Dell XPS 13][xps].

My primary phone is a [iPhone SE][se]. I use an old Moto Z Play as my secondary phone for my work. I backup all of my media to my home server (NextCloud). Other than this, I own a [Kindle Paperwhite][pw3]. For my music, I have a pair of [Jaybird X3][jaybird], alongside the noise-cancelling [Sennheiser HD 4.50][btnc].

I own a [Leopold FC660C][fc660c] keyboard (Topre switches) which I use at work (quieter). My keyboard at home is a [Cooler Master QuickFire Rapid-i][quickfire] mechanical keyboard (Cherry MX Brown). I have a [dual][curved]-[monitor][lguw] setup at home ~~and a Dell Ultrasharp at work~~. I am an ocassional gamer and use the [Logitech G300s][g300s] at both work and office (its [heavily customizable][ratslap]). I also have a [Steam Controller][steamcontroller] and a few more [fancy][airmouse] [keyboards][riitech] for my HTPC.

At home, I have a Raspberry Pi 4 and a PC/HomeServer, which runs lots of tiny services, which are proxied over to the internet with a Digital Ocean droplet in the `BLR1` region. I wrote about it in [detail][homeserver]. The Pi is used for few Kubernetes experiments.

I am also a speedcuber; my primary cube is a stickerless Gans 356 R (Magnetic). I also own several other twisty puzzles, including a Axis Cube and a Megaminx.

## Homeserver

I self-host a lot of things, and my homeserver runs Arch with lots of disks on RAID1. Total usable space is currently around 12TB, and I use it for all sort of things. The server runs [steamos-compositor-plus](https://aur.archlinux.org/packages/steamos-compositor-plus/) and Kodi as the session manager. With [SteamPlay/Proton](https://store.steampowered.com/steamplay), almost everything in my library is playable on Linux, and it makes for a great console. Hardware details are at </setup/homeserver/>.

## And what software?

(audio warning - click to play)

<video
src = "/videos/spectrum_320.webm"
width = "100%"
poster = "/img/spectrum/poster.jpg"
onclick = "this.paused?this.play():this.pause();"
title = "Spectrum Visualization Demo."
class = "center-content"

> </video>

My distro for the last 4 years is [Arch Linux][arch] with [i3][i3] as the window manager. My most used tools include: [Neovim][neovim], [Sublime Text 3][sublime], Firefox, and Git. I game using Steam, and purchase DRM free games via Humble Bundle whenever possible. The above animated wallpaper runs via [spectrumyzer][wallpaper-blog].

Most of my work is done in editors, command line, and the browser. A few essential extensions on my browser include: [dotjs][.js] (with apache support), [Privacy Badger][privacybadger], [uBlock Origin][ublock], HTTPS Everywhere, and Markdown Here. I manage my passwords using [pass][pass].

I am a [Hacker News][hn] addict, and have even [written an application][hackertray] for it. Most used webapps would be: Slack, GitHub. I use [Gonic][gonic]/[play:sub][playsub] for listening to music on the go, and Clementine on the desktop. My security setup (passwords/2FA etc) is documented [here][security].

I run lots of tiny services on my homeserver, including [Gitea][gitea], OpenVPN, Emby, and Grafana. I have my Kindle jailbroken and run [KOReader][koreader] that lets me read EPUBs.

## What would be my dream setup?

A lightweight laptop with tons of battery life, 13" display, and official Linux support (Dell XPS13 DE comes close).

If we're talking super-crazy, I'd love to have a thought-dictation feature. That would help _a lot_ with my writing.

[airmouse]: https://www.amazon.in/gp/product/B083R52QL6/
[galago]: https://system76.com/laptops/galago
[moto]: https://www.motorola.com/us/products/moto-z-play
[hd-202]: http://en-us.sennheiser.com/over-ear-headphones-hd-202
[g300s]: http://support.logitech.com/en_us/product/g300s-gaming-mouse 'Lots of buttons, which I use for my window manager'
[x100]: https://secure.logitech.com/en-hk/product/x100-mobile-wireless-speaker 'Its not very loud, but very good for indoor use'
[quickfire]: http://gaming.coolermaster.com/en/products/keyboards/rapid-i/ 'The backlighting on this keyboard is insanely customizable'
[thunderclap]: http://www.speedcubereview.com/qiyi-thunderclap.html 'No backup cubes at present'
[arch]: https://www.archlinux.org/ 'Rolling, lightweight distro for Linux'
[i3]: http://i3wm.org/ 'i3 is a tiling window manager'
[neovim]: http://neovim.io/ 'Fork of vim for modern platforms'
[sublime]: https://sublimetext.com/3
[hnapp]: http://aws-hn.premii.com/about/ 'Supported on web, iOS and Android platforms'
[adaway]: https://sufficientlysecure.org/index.php/adaway/ 'Blocks ads on android devices using host files'
[afwall]: https://github.com/ukanth/afwall 'AFWall is a firewall for Android'
[ublock]: https://github.com/gorhill/uBlock/ 'uBlock Origin'
[privacybadger]: https://www.eff.org/privacybadger 'Privacy Badger (by EFF) blocks spying ads and invisible trackers'
[hn]: https://news.ycombinator.com 'Hacker News'
[josd]: https://josd.captnemo.in/ "Joy of Software Development, Book I'm working on"
[pirunner]: https://github.captnemo.in/pirunner
[.js]: https://github.captnemo.in/dotjs 'This is my fork of the original dotjs that runs on top of local Apache with a working SSL Certificate'
[libreelec]: https://libreelec.tv
[hackertray]: https://github.captnemo.in/hackertray 'HackerTray is a app-indicator based status menu app for Hacker News (linux)'
[koreader]: https://github.com/koreader/koreader 'Document reader for Kindles that has EPUB and PDF Reflow support'
[wallpaper-blog]: /blog/2017/05/01/spectrumyzer-visualization/ 'I wrote a blog post about how I made my animated wallpaper'
[fc660c]: https://deskthority.net/wiki/Leopold_FC660C "I haven't typed enough on it yet to have an opinion"
[ug]: https://lineage.microg.org/ 'Access all the Google services without proprietary closed software'
[homeserver]: https://captnemo.in/blog/2017/09/17/home-server-build/
[gitea]: https://git.captnemo.in
[airsonic]: https://airsonic.github.io/ 'Free and Open Source community driven media server, providing ubiquitous access to your music.'
[audinaut]: https://f-droid.org/en/packages/net.nullsum.audinaut/ 'Stream music from Airsonic servers.'
[playsub]: https://itunes.apple.com/us/app/play-sub-music-streamer/id955329386 '‎play:Sub Music Streamer on the App Store'
[pass]: https://www.passwordstore.org/ 'The unix password manager'
[riitech]: http://www.riitek.com/product/i8.html 'Mini Wireless Keyboard / Touchpad'
[lguw]: https://www.amazon.in/dp/B01BV1XB2K/ 'LG 25UM58'
[pw3]: https://en.wikipedia.org/wiki/Amazon_Kindle#Kindle_Paperwhite_(3rd_generation) 'Paperwhite 3rd Generation'
[se]: https://support.apple.com/kb/SP738?locale=en_US 'iPhone SE - The Best Phone Apple ever made'
[jaybird]: https://www.amazon.com/Jaybird-Wireless-Bluetooth-Sports-Headphones/dp/B01M7NCT5O
[ratslap]: https://github.com/krayon/ratslap/ 'RatSlap: Linux configuration tool for Logitech G300S'
[curved]: https://www.amazon.in/Samsung-23-5-inch-Curved-Monitor/dp/B01GFPGHSM/ "Samsung's 23.5 Inch Curved Monitor"
[btnc]: https://en-uk.sennheiser.com/wireless-headphones-bluetooth-noise-cancelling-hd-4-50-btnc "Sennheiser Wireless Headphones Noise Cancelling (HD-4.5BTNC)"
[nuc]: https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc8i7beh.html "Very pricey, but totally worth it"
[xps]: https://www.dell.com/learn/in/en/indhs1/campaigns/in-en-dhs-xps-13-9370 "Yes, I have the older edition with the nosecam"
[steamcontroller]: https://store.steampowered.com/app/353370/Steam_Controller/
[security]: /blog/2020/01/04/security-setup/