---
layout: post
title: My quest to build Muzi
---

For the past 3 years I've been involved in developing a campus-only browser based music solution for IITR called Muzi. It has been an amazing experience, and while I'm no longer involved in the primary development of Muzi anymore, I thought it'd be worthwhile documenting my experience for those who tread these waters.

##The start
Muzi started out, like most things in lab, not because we wanted to build this new music player, but because me and pranav happened to chance across this awesome little library called soundmanager and tried to build something out of it. Pranav showed me a few demos, and we started working on a music app, knowing that this clearly had potential. A lot of initial development work was done when we had yet to migrate to git (this is from 2011 Jan), and I don't have the history from back then. 

The first commit was on 2nd March 2011, and by then Shobhit Sir had christened the player as Muzi, a name which would stick.

##The plan
There were a lot of different plans for muzi, depending upon who you asked. For Shobhit or Shashank, it was probably launching with zero bugs asap. For me and pranav, though, it was always building a cool player that someone would ditch their Winamp for. For that to happen, Muzi had to do all of the following:

1. Be easy to use.
2. Be pretty
3. Have a great collection
4. Be fast, even for those on slow connections
5. Be browsable, _exactly_ like your desktop music player

The fifth requirement was often pressed by me scrupulously.

##The architecture
As a result of my PHP background, muzi started out as a dumb-JS client that just a single communication endpoint. That endpoint would decide what data to pass on, depending upon a query param. As it grew in complexity, and as I learned the ins and out of JavaScript (pranav was already quite good at it), it shifted to a JS-heavy client