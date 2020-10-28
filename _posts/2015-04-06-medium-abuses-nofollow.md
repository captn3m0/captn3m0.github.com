---
tags:
  - medium
  - nofollow
  - www
title: Medium abuses nofollow
layout: post
---

**Update**: Since I published this post, I have changed my opinion somewhat on the matter. This post is [quite confrontational](https://news.ycombinator.com/item?id=9328384) and I didn't mean it to be that way. Medium is not wrong in this matter, but I still think we need to look for better solutions. I have since been working on a [proposal/idea](https://github.com/captn3m0/ideas/blob/master/BADIDEAS.md#-nofollow-enforcer) that would use machine learning to "solve" this problem, instead of side-stepping it.

I call <a href="https://medium.com" rel="nofollow" title="This is a nofollow link">medium</a> a "_mostly good_" platform for lazy writers. A lot of people have written about its excellent typography, or it being the next "big publishing platform". I've used medium in the past, and while it does have its benefits, I have stopped using it.

My primary reason was that I already have a blog, where I can control the entire experience. This is the same reason why New York Times does not start publishing articles on Medium.

The other reason is nofollow abuse.

Medium hosts more than [1M indexed pages](https://www.google.co.in/webhp?q=site%3Amedium.com#q=site:medium.com). It has around [650k users](https://medium.com/editors-picks) currently by [a conservative estimate](https://www.quora.com/How-many-users-does-Medium-have/answer/Josh-Yang). Rounding it to 700k to account for other users, collections, and other internal pages, it leaves us with around 300,000 articles on medium.

A basic tenet of the web is linkability. That is what Tim Berners Lee meant when he talked about HyperText:

>HyperText is a way to link and access information of various kinds as a web of nodes in which the user can browse at will.

Over time, the web has evolved, and is now not just limited to human users, but to computers as well. This is an important consideration on which the web rests today. The biggest example of this is Google Search, which uses these links to "follow, spider, and index" the web. Google uses this linking information to build a citation index, which gives us the quality of a web page depending on the quality and number of sites that link to it.

If you know a bit or two about SEO, you might have heard of shady backlink techniques, which essentially amount to you getting links from an established site. This often takes the form of user-generated content such as comments and answers.

While fighting spam is important, it is far more important to make sure that web remains linked, that people are credited for the content they create. Medium hosts 300,000 articles published by half a million users, and yet none of these links back to external website, because of something called "rel=nofollow".

When a link has a `rel=nofollow` attribute, search engines do not count it as a citation in their index. While this may be the right strategy for comments on a wordpress blog to prevent spam, this is not the right way to move forward if you want to "revolutionize the publishing industry".

While medium is not as bad as some other sites in this regard (like quora, which even blocks the internet archive), it is very important because it portrays itself as a "publishing platform". This means, medium is made up of articles, blog posts, with lots of outbound links compared to, for instance, StackOverflow answers (which [solved this problem back in 2011](http://meta.stackexchange.com/questions/111279/remove-nofollow-on-links-deemed-reputable)).

If you publish content on medium, and provide relevant links for your readers, remember that these links are not considered as relevant by search engines.

Medium has said that this is [not a top priority](https://twitter.com/lenkendall/status/432203084270292992) at the moment for them.

I understand completely. Handling spam would be a far more harder problem to solve than just blacklisting all outbound links. But we cannot go this way, if we want an open web. We need publishing platforms that cite content, and not blacklist it. This is why I write content on my own blog, and not on medium.