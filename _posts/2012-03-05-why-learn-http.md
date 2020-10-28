---
layout: post
title: Why you should learn HTTP?
tags:
- http
- learning
---

I see people learning RoR, PHP, Django, with a single intent: getting their own website. Of course, it is the million dollar idea that will blow everyone away, as always. But what I find fascinating is that too many upcoming web developers are testing the waters with opinionated coding frameworks. The entry barrier for software development has been lowered exponentially in the last decade, leading to a slew of web frameworks, tutorials, and screencasts. Today is arguably the best time to be involved in software development. Lots of people are learning to code their first web-site with rails, or django. There are lots of benifits with this approach: as a beginner, you are kept isolate from all the complexities, and can focus more easily on your application.

But, it also leads to shallow learning. You could have written a dozen sinatra apps, and still not understand how it all works. And as it stands, it is not essential to learn it. You can easily develop entire websites thinking only in terms of urls, hyperlinks, routes and controllers. This is all good for starting up, when you don't wanna deal with the complexity of it all, but I'd expect any competent web-developer to understand HTTP.

You see, HTTP is the foundation for all of web. It is how the internet tubes work. Learning HTTP is uncovering the hidden layer behind your browser. It is understanding how cookies, and sessions work in PHP; how xsrf attacks happen and mitigating against them; the magic that rails does when it creates objects from the submitted form parameters transparently for you. And the best part is that its not all that difficult to learn at all.

There was a [lot of debate concerning REST recently](http://news.ycombinator.com/item?id=2724488). I don't claim to understand REST fully. I'm yet to meet someone who does. But I can comfortably build RESTish APIs, and consume them with ease without breaking a sweat. And smile at the fact that its all just HTTP. You cannot move to REST, [HATEOAS](http://en.wikipedia.org/wiki/HATEOAS) unless you are comfortable with HTTP.

So, if you are a beginner in web-development, here's my advice to you: Understand HTTP. A few pointers:

- Read [a good](http://shop.oreilly.com/product/9781565925090.do "HTTP: The Definitive Guide") [book](http://shop.oreilly.com/product/9781565928626.do "HTTP Pocket Reference") on HTTP.
- Read the [HTTP RFC](http://www.w3.org/Protocols/rfc2616/rfc2616.html).
- [Wikibooks](https://en.wikibooks.org/wiki/Communication_Networks/HTTP_Protocol) and [Wikipedia](http://en.wikipedia.org/wiki/Http) entries on HTTP are quite good.
- Use the network tab in Webkit Inspector/Firebug. And understand each of the damn headers.
- Start using `curl -i`, if you don't already
- Above all, be curious

Question the web.
