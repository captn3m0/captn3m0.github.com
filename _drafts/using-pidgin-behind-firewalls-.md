---
title: Using Pidgin Behind Firewall
layout: post
---
I've been trying to use Pidgin for quite some time. I even got Google Chat to work. However the same could not be said for my facebook account. I could never get it to work, not matter how much I tweaked my settings. I finally figured it out, with a little help from @Shobhit Singh.

Here are the simple settings. Anything not written down, must remain unchanged.

####Google Chat
{% highlight yaml %}
Protocol: XMPP
Username: <your username>
Domain: gmail.com
Password: <your password>
Connection Security: Use old-style SSL
Connect Port: 443
Connect Server: talk.google.com
{% endhighlight }

####Facebook Chat
{% highlight yaml %}
Protocol: XMPP
Username: <your username>
Domain: chat.facebook.com
Password: <your password>
Connection Security: Require Encryption
Connect Port: 5222
Connect Server: talk.google.com
{% endhighlight }

I'm not sure why it would not work earlier, but it does now. Also if you use Google Talk/Facebook Chat protocol while creating a new account, it would automatically save it as XMPP finally. So you can directly create an XMPP account and be done with it.
