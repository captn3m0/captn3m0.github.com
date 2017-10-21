---
title: Building the perfect audio visualization
layout: post
tags:
- visualization
- audio
- python
---

I made this as my animated wallpaper recently (Click to play/pause):

<video 
    src = "/videos/spectrum_320.webm"
    width = "320"
    poster = "/img/spectrum/poster.jpg"
    onclick = "this.paused?this.play():this.pause();"
    title = "Spectrum Visualization Demo."
    class = "center-content"
></video>

_above video has a audio component, click at your own peril_.

What follows is the story and the tech behind making this.

## The Wallpaper

I have a long history of using custom wallpapers. This was my wallpaper from 2014-:

![Old Wallpaper][wallpaper.old]

When I asked [Vikalp][vikalp] to design a new one, I knew I wanted something that
was slightly more softer. This is what he came up with, after a few iterations:

![New Wallpaper][wallpaper.new]

This wasn't the final iteration, and both of us agreed that there was something missing.

## Visualizations

I saw a colleague using [`cava`][cava] and spent a bit of time trying out different
visualization software. The ones that I tried out:

**[cava][cava]**
: works perfectly with i3, runs on a terminal. I couldn't get it to work cleanly with transparency. ![Cava screenshot using tiling][img.cava]{:#cava: .center-content}

**[mildrop][milkdrop]**
: Winamp's legacy. This works great for parties, but is not really an everyday-use visualizer. ![Milkdrop Running using projectM on Linux][img.projectm]{:#milkdrop: .center-content}

**[spectrumyzer][spectrumyzer]**
: Worked with transparency, but limited to bars visualization.

I decided to go ahead with Spectrumyzer (This is the default config):

![Default Spectrum Config][spectrum.default]{:: .center-content}

## The Traffic Jam

The very same day, stuck in a traffic jam[^3], I asked Vikalp for some color ideas on the visualization.

The obvious 2 were tried first:

![Spectrum Dark Blue Config][spectrum.darkblue]{:: .center-content}

![Spectrum Yellow Config][spectrum.yellow]{:: .center-content}

It finally dawned on us to use the light blue variant with padding set to zero:

![Spectrum Light Blue][spectrum.blue]{:: .center-content}

Here is one showing the actual positioning (set using the offsets):

![Spectrum Offset][spectrum.offset]{:: .center-content}

## Bezier Curves

With the padding set to zero, it already looked great. I ended up using this
as my wallpaper for the next one week. Vikalp wanted to make the bars
non-rectangular, and I spent some time figuring out how to make waveforms using 
bezier curves[^1]. The basic learning from my experiments were:

- Cairo has methods for drawing cubic bezier curves.
- Cubic bezier curves have 2 control points.
- The control points must be symmetric (equidistant) as well as parallel to the origin points.
- The parallel part ensures that the ending and starting line segments are always tangential giving a smooth joining.

This is roughly what you want to do when drawing waveforms:

![Waveform bezier curve][waveform]{:: .center-content}

If you are interested in playing around with Bezier curves, see [Animated Bézier Curves][bezier.animated]. [A Primer on Bézier Curves][bezier.primer] is a math-heavy explanation if you want to read further[^2].

The code I wrote picks the midpoints of the bars and then connects them using bezier curves:

```python
# control point cords
# Make sure these are symmetric
c1x = rect_top_mid_x + 16
c2x = next_rect_top_mid_x - 16
c1y = rect_top_mid_y
c2y = next_rect_top_mid_y
```

I also had to make the number of bars configurable (this is default=64, which doesn't look great):

![Spectrum water 64][spectrum.64water]{:: .center-content}

Here is the complete final result in HD:

<iframe
    width="560"
    height="315"
    src="https://www.youtube.com/embed/_vWe_AHAJCk?rel=0"
    frameborder="0"
    allowfullscreen
    class="center-content"
></iframe>

## What I learned

- Bezier curves are not magic.
- Drawing pixels on screen and filling them was quite easy with Cairo and Python.
- Coding is wizardry. The things that I take for granted every day (take a multi-page website and get useful tabular data out of it, for eg) are unthinkable for most people. The idea of doing water waves was something I knew would be possible before I even looked at the codebase.

If you'd like to replicate this setup, or build upon it, here is my [spectrum.conf][config] file.
I also [filed a PR][PR] (now merged!) to the spectrumyzer project adding support for curve based renders.

[^1]: The Spectrumyzer codebase turned out to be fairly easy to understand. It was just cairo and pyGTK.
[^2]: [A Primer on Bézier Curves][bezier.primer] was published on HN just a few days after I finished this project.
[^3]: [Sony World Junction][twitter.sonyworld] - Where startup ideas are born.

[twitter.sonyworld]: https://twitter.com/SonyWorldJn
[wallpaper.old]: https://cdn.rawgit.com/captn3m0/avatars/a8255290/wallpaper/1920x1080.jpg
[wallpaper.new]: https://cdn.rawgit.com/captn3m0/avatars/a8255290/wallpaper/minimal.jpg

[spectrum.default]: /img/spectrum/default.jpg "Spectrumyzer Default Config"
[spectrum.poster]: /img/spectrum/poster.jpg
[spectrum.darkblue]: /img/spectrum/darkblue.jpg "Spectrumyzer Dark Blue Config"
[spectrum.yellow]: /img/spectrum/yellow.jpg "Spectrumyzer Yellow Config"
[spectrum.blue]: /img/spectrum/blue.jpg "Spectrumyzer Blue Config with zero padding"
[spectrum.offset]: /img/spectrum/offset.jpg "Spectrumyzer offset configuration"
[spectrum.64water]: /img/spectrum/64water.jpg "Spectrumyzer curves config doesn't look that great with 64 bars"

[waveform]: /img/bezier.waveform.gif
[bezier.animated]: https://www.jasondavies.com/animated-bezier/ "Animated Bézier Curves, Play with the control points to modify the curves!"
[bezier.primer]: https://pomax.github.io/bezierinfo/ "A Primer on Bézier Curves, A free, online book for when you really need to know how to do Bézier things."
[cava]: https://github.com/karlstav/cava#arch "Console-based Audio Visualizer for ALSA (MPD and Pulseaudio)"
[vikalp]: http://vikalpgupta.com/
[milkdrop]: http://projectm.sourceforge.net/ "MilkDrop was the hardware-accelerated music visualization plugin for Winamp. ProjectM is the port that doesn't need Winamp and works on linux"
[spectrumyzer]: https://github.com/HaCk3Dq/spectrumyzer/
[img.cava]: https://cdn.rawgit.com/karlstav/cava/gh-pages/cava_gradient.gif
[img.projectm]: /img/milkdrop.jpg
[config]: https://github.com/captn3m0/dotfiles/blob/master/files/audio/.config/spectrum.conf "Just ensure you have the latest spectrumyzer code before using this"
[PR]: https://github.com/HaCk3Dq/spectrumyzer/pull/22 "Configurable renderers"