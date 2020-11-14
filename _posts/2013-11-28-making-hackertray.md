---
layout: post
title: Making HackerTray
tags:
- python
- gtk
- application
- hacker news
---

A few days back, I found the excellent [HackerBarApp][hb] via Hacker News. Hacker News,
for those of you who don't know, is  tech news website run by [YCombinator][yc].
Hacker Bar was the simplest way of accessing HN stories that I'd ever seen. Unfortunately,
it was only for Mac (made using [rubymotion][rm]) and even though the source was available,
it was of no use to me as a Linux User.

I decided to make a clone of Hacker Bar that would work on Linux. My first choice of the
stack was [node-webkit][nw], an application framework that allows you to build cross-platform
applications using HTML, CSS, JS, and modules from the node.js ecosystem. After reading a lot
about node-webkit, I figured out that building this application in node-webkit (as it stands)
would not be possible. Or rather, it would not work under Ubuntu and its derivatives because
of lacking appindicator support in [node-webkit][1087]. More details [here][google-group-link].

The next obvious language and stack of choice was Python + Gtk. I'd already played a little bit
with Gtk and Python some time back, so I knew the basics. But I'd never build a real application
with PyGtk, just toys and small scripts. I found a [basic skeleton app](http://www.eurion.net/python-snippets/snippet/Create%20an%20Application%20Indicator.html)
that was written for AppIndicator and modified it somewhat to form the base of HackerTray.

The next challenge I faced was keeping the check boxes always checked despite of any number
of clicks after the first. That is, we don't want any menu item to be "un-checked" at
any moment. A basic idea is to do this (partial code):

{% highlight python %}
def open(self, widget):
	if(widget.get_active() == False):
		widget.set_active()
	webbrowser.open(widget.url)

def addItem(self, item):
	#create a new CheckMenuItem (i)
	i.connect('activate', self.open)
{% endhighlight %}

However, this does not work as expected, because the `widget.set_active()` call also results
in the `activate` event being fired, which ultimately calls `open`. This means on a click to
an unchecked menuItem, the open function is called twice. This results in the browser opening
the link twice.

As a workaround, I disabled the event handler in case it is a checked menuItem:

{% highlight python %}
def open(self, widget):
	if(widget.set_active() == False)
		wiget.disconnect(widget.signal_id)
		widget.set_active(true)
		widget.signal_id = widget.connect('activate', self.open)
	webbrowser.open(widget.url)

def addItem(self, item):
	#create a new CheckMenuItem (i)
	i.connect('activate', self.open)
	i.signal_id = i.connect('activate', self.open)
{% endhighlight %}

The next thing I worked on was a persistent memory for the app. In a nutshell, I needed to
make sure that the tick on an item remained there, even if the app was restarted. This meant
writing a list of all the "viewed" items into a file. After looking at [shelve][shelve] for a
bit, I just [rolled my own implementation](https://github.com/captn3m0/hackertray/commit/167397e51f665847400617935653027ebba0b396)
, based on storing the data into `~/.hackertray.json` file.

After that I worked on packaging the app into a python package, so that it could be easily installed.
The [python packaging tutorial](https://python-packaging.readthedocs.io/en/latest/) was an easy to use guide
that let me [create the package](https://github.com/captn3m0/hackertray/commit/6ca735ea089d9189f152612ed016d31d72f9c36b)
easily and push it to the [Python Package Index](https://pypi.python.org/pypi/hackertray/). A few issues in the package
were found, and were fixed quickly thanks to [the pull request](https://github.com/captn3m0/hackertray/pull/7) by [@brunal][brunal].

After improving the README a bit, I posted about it on Hacker News, where it failed to get any traction. I re-tried with a link
to the HackerTray website, and that fell flat as well. It was on the next day, when I [posted it to HN](https://news.ycombinator.com/item?id=6819042)
for the third time, that it took off. After 50 or so upvotes, I found that my instance refused to run because it had
hit the API Rate Limit on the excellent [node-hnapi](https://node-hnapi.herokuapp.com/). I quickly [pushed a fix](https://github.com/captn3m0/hackertray/commit/8f0b08137b6c4b05ebe63a33029a36c068cfbc05)
that used a list of servers to hit as fallback in case it crossed the Rate Limits.

After a lot of feedback from HN, I started work on a `node-webkit` based clone of hackertray for Windows. I should be able to release
it in a few more days, if nothing else crops up. Keep watching this space for info. If you have any queries, just [file an issue on GitHub](https://github.com/captn3m0/hackertray/issues/new)
or [contact me](mailto:capt.n3m0@gmail.com).

[hb]: http://hackerbarapp.com/
[yc]: http://ycombinator.com
[rm]: http://www.rubymotion.com/
[nw]: https://github.com/rogerwang/node-webkit
[1087]: https://github.com/rogerwang/node-webkit/issues/1087
[google-group-link]: https://groups.google.com/d/topic/node-webkit/FeX7YYwK8jI/discussion
[shelve]: http://docs.python.org/lib/module-shelve.html
[brunal]: https://github.com/brunal