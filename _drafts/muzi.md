---
layout: post
title: Muzi - the little things
---

This was supposed to be a post about Muzi, the browser based music player I made at [SDSLabs][]. However, I decided that instead of writing about the creation process, it would be cool to document the many little things we implemented in Muzi to give the best possible experience we could.

##Keyboard Shortcuts
We used shortcuts from existing player, creating our own when there were no alternatives available.

![List of Shortcuts](/img/muzi/shortcuts.jpg)

The shortcuts help screen is shown when you press either `?` or `F1`.

##Loading bar
The seekbar uses a grey color to denote the loading progress of the song. This is especially useful if you are on a slow network, and it tells you how far the song has buffered. The seekbar is overlayed on top of the loading bar.

Fun fact: Earlier the loading bar got updated thousands of time per second, and then we realized that such preciseness was unneeded, and then shifted to a 0.5s timer, which would update the seekbar and loading bar on every tick.

![Seekbar in loading state](/img/muzi/seekbar.png)

##Caching
Muzi aggressively caches everything it can. All the data is cached to localStorage, and localStorage is cleared on every reload. This is done as an easy way to handle cache invalidation. We also use memcache on the backend to cache some long-running queries. Caching on the frontend is not just limited to the app, but also to static assets as well. This is why sometimes you can listen to complete songs even though you are offline.

The end result is a much simpler and faster experience.

