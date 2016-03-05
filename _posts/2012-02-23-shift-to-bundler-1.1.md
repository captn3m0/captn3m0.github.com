---
layout: post
title: Shift to bundler 1.1 (Ruby)
tags: 
- ruby
- bundle
- snippet
---

In case someone out there is still stuck with bundler `1.0`, and hates seeing the `Fetching source index for http://rubygems.org/.` screen, please update to `bundler 1.1`.

The following command should do the trick:

    gem install bundler --pre

Bundler 1.1 is faster by a huge margin in comparision to 1.0.

### References

- <http://patshaughnessy.net/2011/10/14/why-bundler-1-1-will-be-much-faster>
- <http://robots.thoughtbot.com/post/2729333530/fetching-source-index-for-http-rubygems-org>
