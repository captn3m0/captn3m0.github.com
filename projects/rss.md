---
permalink: /projects/rss
layout: page
title: RSS Projects
---

List of RSS (Rich Site Summary) related projects that I've worked on:

[Core OS Container Linux Releases RSS Feed](https://github.com/RSS-Bridge/rss-bridge/pull/718)
: Made a RSS Feed for Core OS releases. Now made useless by CoreOS going EoL.

[Amazon Price Tracker RSS Feed](https://github.com/RSS-Bridge/rss-bridge/pull/741)
: This isn't 100% functional, but the idea is to get a new RSS notification every time the price goes down.

[SEC Filings RSS Feed](https://github.com/RSS-Bridge/rss-bridge/pull/1011)
: The SEC website has filings for all public companies. This converts it into a RSS-feed, so you can get notified as soon as a company files something. Useful for investors, I'm told.

[Apple AppStore Apps Bridge](https://github.com/RSS-Bridge/rss-bridge/pull/1316)
: Ever wanted to get notified when an application has a new release on the App Store? Now you can! And pipe it to Slack if you'd like. Use it to track competitors and the like.

[BookMyShow Bridge for RSS](https://github.com/RSS-Bridge/rss-bridge/pull/1349)
: Want to get a notification when a new movie starts screening? Or when a new play shows up in your town? BookMyShow RSS feeds. Needs a few more changes before I can merge this upstream.

[Goodreads Bridge for RSS](https://github.com/RSS-Bridge/rss-bridge/pull/1559)
: Goodreads has some RSS Feeds, but was missing one for authors. This lets you get notified as soon as your favorite author publishes a new book. Not yet merged upstream

All of the above are usable at my [rss-bridge server][bb8].

[OPML Generator](https://github.com/captn3m0/opml-gen/)
: Generates a OPML feed fom a few sources:
  - GitHub releases RSS feeds for all your starred repos.
  - SEC Stock Filing RSS feeds for multiple stock tickers.

The idea was to support a way for users to generate OPML feeds to easily migrate off other platforms. I also help maintain the Docker image for rss-bridge. I don't guarantee any uptime for my RSS Bridge server, and there are a few other public hosts with more bridges enabled at <https://github.com/RSS-Bridge/rss-bridge/wiki/Public-hosts>


[bb8]: https://rss-bridge.bb8.fun "My RSS-Bridge server."
