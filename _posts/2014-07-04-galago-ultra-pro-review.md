---
layout: post
title: A month with the System76 Galago Ultra Pro
tags: 
 - system76
 - laptop
 - review
---
With my recent [CCTC Winnings](/blog/cctc-wave-3/), I decided to purchase a new laptop as my old Dell Inspiron was not performing up to the mark. Being of a time before the Intel i-series launch, it was also severely lacking in several features, most notably virtualization support, which is badly needed these days.

After taking a thorough look at the various offerings in the market (and being disappointed by most of them), I decided to go with the [System Galago Ultra Pro][galago] for the following reasons:

- Linux Support (Just Ubuntu actually, but its nice to have a laptop that supports and comes with Linux pre-installed).
- Intel HD 5200 Graphic Card. Even though the nVidia/ATI support has been getting better in Linux these days, I wanted a graphic card that I could use without worry, for both playing games, using webGL without having to worry about things like overheating and switching card modes (optimus/bumblebee and whatnot).
- Haswell. Not many manufacturers are currently offering Haswell lineups, and System76 is one of the few with them in the market.

The other few machines I did consider included the Apple MBP, Lenovo Ideapad, Dell Sputnik 13. The MBP was rejected because I wanted a Linux machine, and it was overly costly; the Ideapad had a touch screen, which I abhor; and finally the Sputnik is too expensive as well.

A few other machines were rejected because I was exclusively looking for a 14-inch screen, due in part to my experience with my previous bulky machine.

##Hardware Review
The build quality of the Galago is above average, but its still a flimsy offering, when compared to the MBP or other business class offerings such as the Vostro. A lot of the Galago reviews on the internet talk about the defective keyboards, but I faced no such issues. It seems to have been fixed, and the keyboard has been iterated several times since, I think.

The IPS screen (1920x1080) is a real gem, and I've gotten used to watching everything in full HD these days. The laptop has 2 small fans on the lower side, and they hardly ever kick in, making it a quiet laptop. The only times it heats up much is when I'm playing demanding games or doing something GPU intensive. A few issues that I've actually faced with it include:

- The `Esc` key not responding to all presses. I have to hit it with a slightly extra pressure for each keypress to register. However, this is just a quirk I've come to accept, and work around. My muscle memory soon overtook and I'm now used to pressing it hard.
- Missing Media keys. It does have the usual Mute, Volume, and the Play/Pause keys, but the next/previous media keys are missing on the keyboard.
- The charger getting heated up (a lot). It even heats up when the charger is not connected to the laptop.
- The inbuilt speaker quality is definitely not above average. I usually use my earphones with it, so its not much trouble to me anyway.
- The "clickpad" becomes a "touchpad" in Windows, which means drag-drop becomes extremely uncomfortable if you're not used to it. I've installed the official touchpad drivers in Windows from knowledge76, but I could not find a setting to use "clicks" instead of "touch".

As an aside, I really like the keyboard layout (I don't like numeric keypads much) and the placement of Del-End keys, which is incidentally same as my previous laptop. I really dislike those layouts where you have to press a combination of Fn+Some key just to trigger Page Up/Down. A note to laptop manufacturers : [Please stop messing with the keyboards](http://arstechnica.com/staff/2014/01/stop-trying-to-innovate-keyboards-youre-just-making-them-worse/).

Having a branded Ubuntu key is also a good show-off at some places :) I also have to mention that the laptop is very silent. The fans rarely kick in, and I have faced no heating issues so far.

##Software Side
Despite being built for Linux, I've still faced a few software issues on Linux. None of these are a deal-breaker though for me. The first time I realized that it wasn't really built for Linux was when I booted using my external to Ubuntu 12.04 and the WiFi didn't work. Apparently you need a combination of System 76 custom (though open-source) drivers and 14.04 on this machine to get the drivers to work. This is one of the reasons I haven't downgraded to Elementary Luna (which is based on Ubuntu 12.04). The issues I've faced (along with my workarounds) include:

- Flash not working on Google Chrome Stable. I talked to System76 support over this, and I'm yet to get it working. As a workaround, I've been using Google Chrome Unstable (which I usually use anyway), and it detects flash fine.
- WebGL support in Chrome is a bit sketchy. Chrome stable doesn't detect the graphic card as supported, while the Chrome Unstable version did detect it as working for a while, but the graphic card was either removed from the whitelist, or added to the blacklist in a future update, making it non-working again. Currently, I'm using the "Disable WebGL Blacklist" flag from `chrome://flags` to get it working.
- Webcam not being detected. This has gotten me a bit puzzled. It was working fine on the fresh Ubuntu 14.04 setup, but some driver issue is preventing it from working now. I think a dist-upgrade should fix it, but I'm not sure. I might try to re-install the `system76-driver` package if that doesn't work. **Update**: It started working again after just a restart.
- Another minor issue I face is that the brightness key on the keyboard (Fn+F8/F9) allows you to take the brightness level all the way down to *zero*. So you could make your screen pitch-black, with absolutely no idea how to get it back to normal. This happens only on ubuntu, though.

##Overall
Despite its few quirks, I'm liking my new laptop. I'm enjoying gaming on it (on both Linux and Windows), and it has more than enough power to run whatever combination of VMs I want to. 

##Gaming
All the Linux games from my various Humble Bundle purchases are finally being put to good use. The only game that I haven't been able to run is Oilrush, which doesn't support Intel Graphic cards on Linux for some reason. Some of the games that I've tried and enjoy on Linux include:

- Mark of the ninja
- The Swapper
- Don't Starve
- Fez
- Bit Trip Runner 2
- Counter Strike: Source
- Portal
- Half-Life 2
- Civilization 5
- Trine 2
- Minecraft

Trine 2 does show some noticable lag on full settings, but its not supported on Intel drivers anyway. Rest of the games run wonderfully on full settings.

I haven't tried gaming much on Windows, but I do play Blur (admittedly a 3 year old game) sometimes on it at the highest settings.

##Specs
The only thing I upgraded in my laptop was an increase in RAM from the default of 4GB to 8GB, primarily because I intend to run lots of VMs on this machine. The rest is same as the specs [on the official site](https://system76.com/laptops/model/galu1) (scroll to bottom):

```
Processor: Intel(R) Core(TM) i7-4750HQ CPU @ 2.00GHz
RAM: Samsung, SODIMM DDR3 Synchronous 1600 MHz (0.6 ns), M471B5173QH0-YK0 (4GiB) x2
Graphic Card: Intel Iris Pro Graphics 5200 with 128 MB eDRAM, Crystal Well Integrated Graphics Controller
Hard Disk:  Western Digital, WDC WD5000LPVX-2, 500GB (465GiB)
Operating System: Ubuntu 14.04 (Pre-installed)
Desktop Environment: Pantheon, using the elementary-os-daily PPA
Memory: 8GB 204 pin Dual Channel DDR3 @ 1600 MHz
```
If you're interested in getting any further details about the laptop, feel free to [contact](/contact/) me.
