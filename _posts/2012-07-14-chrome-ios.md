---
title: "Things I expect in a Chrome/iOS update"
layout: post
tags: 
- chrome
- ios
---

I've changed to using Chrome for iOS as my primary browser. Since I only own an iPad 2, all of my observations are with regard to the iPad version of the browser.

##Why I love Chrome

Chrome is already my primary browser on my primary machine, and after it came out for the iOS, I tried it out hesitantly, but to my surprise (contrary to what the internet says) it is working out even better than expected.

- Ability to sync tabs across my laptop and tablet. I can leave my laptop and continue reading on the go. I don't own a Mac, so I can't comment against how Safari/iCloud does it, but it works well enough for me.
- All my desktop bookmarks (and bookmarklets) are available and functioning instantly.
- Omnibox is awesome, and saves me a lot of trouble, looking in my history, bookmarks, and pre-fetching stuff. This was the most important feature that Chrome v1 brought along with it (when it was released in Windows), and its nice to find it work exactly as indended.
- Incognito Mode (I previously used Dolphin in private mode, but this is far better).
- Complete bookmark listing while creating a new bookmark. Unlike Desktop version of Chrome, which only shows 5 most recently used folders. I bookmark stuff extensively, and it makes the process much easier for me than on the desktop version, ironically. [See Image for Comparision](/img/bookmark_compare.png)
- Tab Switching is brilliant. It seems to be inspired/copied straight from [Paper](http://itunes.apple.com/us/app/paper-by-fiftythree/id506003812?mt=8), but it is executed well enough for me. It gets better once you get used to it. The tag bar itself is scrollable as a plus (you can hide/unhide tabs). I've read people complaining about this, but it helps me browse on the ipad one-handed.
- It feels fast, especially after continous use. I don't know if its the ported networking stack, or better caching, but page load speeds are better than Safari for me in general.

**Note**: If you have a jailbroken device, you can setup Chrome as your default browser using BrowserChooser from Cydia. The best part is that home-screen shortcuts open in Chrome as well.  I've ditched Facebook App for a shortcut icon to `touch.facebook.com` as a result.

##Things I want

- Support for **configurable search engines**. I use them extensively (for eg **d**uckduckgo, google **l**ucky search, **a**mazon, **e**bay, **g**it**h**ub, **s**tack**o**verflow and even google **m**obile search). The pre-defined search engines are of no use to me (Bing/Yahoo/Guruji).
- **Find in Page**. This is a no-brainer. **Edit**: This is available via [Chrome Customizer](http://www.addictivetips.com/ios/great-cydia-tweaks-for-chrome-iphone-ipad/) in Cydia for a jailbroken device.
- Ability to **turn off images/javascript**) (Content Settings). I'm not sure if it will be possible w/o proxying like how Opera does, but this would be nice to have (since people might want to save bandwidth on 3g).
- Support for emailing an entire page (rendered).
- **UserScript support**. I don't know if apple would allow it at all, but I think the Apple ToS disallows code to be downloaded. What if there were some sort of linking support to allow me to insert some external script tag? 
- **Readability/iReader** like support. The safari readability link does work wonders. This could be simulated with a bookmarklet, but once again calling them is hard. **Update**: ChromeCustomizer can do this via settings menu (see below).
- **Better access to bookmarks/bookmarklets**. At least show me the mobile bookmarks so I can keep them separate.
- Wait a bit more before taking the page snapshot for the speed-dial. The GMail snapshot has always been blank for me. At least check if the snapshot is completely blank, and wait a bit more if that is the case.
- App shortcuts. The kind like you get for almost all websites on Chrome Webstore. I think they are referred to as **"Chrome Apps"** against "Extensions", which would be completely disallowed as per Apple ToS. Since Apps are just shortcuts and some icons, they should be allowed in some manner.
- **Better history** support. Seeing just the last 6 closed tabs kind of sucks. Give me some real history browser (and improve the one in desktop chrome while you're at it).
- Mailto support (for gmail etc). Don't know if possible, but would be nice to have.
- Selection Mailing. Just let me select and mail some html.
- **Handle pdfs** better. By default chrome redirects to Safari for pdfs. After changing Chrome to default, it does handle pdfs fine, but I miss the "Open In iBooks" link. Don't see this happening though. (Update: This was fixed in a Chrome Update)
- **Webintents** support would be nice to have (via something other than chrome Webstore, I Guess)
- **CloudPrint** support. I don't use this, but I am assuming there are people who do.
- **FullScreen** support of some sort. Safari in iOS 6 is bringing this much asked for feature, so there are people who would love to have this. Chrome's faster tab switching should help it out with some of the Full Screen issues. (**Edit**: This is available via a three finger tap if you install [Chromizer](http://www.idownloadblog.com/2012/07/01/chromizer/) from Cydia's ModMyi repo). Chromizer also forces the iPhone style tab switching on the iPad as a side-effect.

There is also a [ChromeURL](http://www.idownloadblog.com/2012/07/01/chromeurl/) tweak available for Jailbroken devices that changes the keyboard layout to the the one used for address bar in Safari (So called tld keyboard). 

Another one called [ChromeCustomizer](http://modmyi.com/content/8108-chromecustomization-adds-some-new-stuff-google-chrome.html) offers the following:

- Add one bookmarklet to the settings menu. I'm using [Readable](http://readable.tastefulwords.com/) at present.
- Adds a [broken](https://github.com/rpetrich/ChromeCustomizer/issues/1) fullscreen implementation (maybe it is clashing with Chromizer) via the Menu. I prefer Chromizer's 3 finger tap for fullscreen.
- Adds a Find in Page feature. **Update**: This is now available
- Adds some filtering for ads/tracking websites.
- Adds an option to change Chrome tab switching mode (iPhone vs iPad).

See [this blog post](http://www.addictivetips.com/ios/great-cydia-tweaks-for-chrome-iphone-ipad/) for some more tweaks available on cydia.
