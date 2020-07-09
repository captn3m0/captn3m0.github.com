---
layout: post
title: Privacy Hacks
---

I sent this to a journalist as part of a Privacy-hacks article, but since not everything was worth including in the article, thought I'd publish the entire list on my blog.

Disclaimer: I don't follow everything documented here to the dot (I only have 2 SIMs for eg).

1. Use a different email address for various services. I run mine on a custom domain (`@captnemo.in`) so that all anything@captnemo.in arrives at my inbox. You can use the "plus" trick for [GMail][0], or just use [FastMail][1] or [Apple Sign In][2]. If you have this, you can just setup a filter to autodelete spam you get from a specific source.
1. Have a separate "dumb" phone/SIM for work and/or services where you sign up. That way, your personal phone number is not exposed to most services you use. I think Kiran was trying a 3-SIM approach:
    - Personal (given out to people you know)
    - Financial (only for financial OTPs)
    - Services (give to everyone, but you don't really care).

1. Run an AdBlocker everywhere you can. It saves battery life, prevents third-parties from tracking you, and genuinely makes the internet worth browsing. Recommended ones are:
    - Browsers: [uBlock Origin][3]
    - iOs: [DNSCloak][4]
    - Android: [Block This][5]

1. Split payments between parties I trust. In particular, while my bank gets to know the majority of my payments (made using my cards), I exclusively use [Simpl][simpl] for a few category of payments, and for those - my bank only gets to see a single line item payment to SIMPL. It is not optimal (I'm now leaking data to 2 parties) but it does mean that all my eggs aren't in one basket. I try not to over-diversify either, and limit financial application usage accordingly.

5. You can disable personalized advertising for most ad companies, including:

    1. Google: <https://support.google.com/ads/answer/2662922>
    1. Facebook: <https://www.facebook.com/help/568137493302217>
    1. Apple: <https://support.apple.com/en-in/guide/iphone/iphf60a6a256/ios>
    1. Amazon: <https://www.amazon.in/adprefs>

6. This is more towards security (than privacy), but ensure that you have a SIM PIN, Encryption, and Passcode setup on your phone.

7. Unlist yourself from TrueCaller: Here's a [guide][6], [and the corresponding link on the TC website][7].

8. Review the "gist" of the Terms and Conditions for various services at https://tosdr.org/ (Terms of Service; Didn't Read)

9. Pay for content but still pirate it. I pay for Netflix, but Netflix doesn't necessarily know what all I watch. It also prevents situations where you can't rewatch a film because [it got pulled][8].

10. Refuse to give your details to [MyGate][mygate]. Type in a bogus phone number and name if you are forced. Enter like you belong and nobody will question you anyway.

11. Ask companies what is happening to your data. Who are they sharing it with? How are they using it? How many people will have access to it.

12. If a company is smaller than 250 people, assume that everyone there will have access to your data.

13. Whatever happens, don't buy a smart device. Especially if it comes with a mic. I treat consumer hardware as a stranger in my house - they must be supervised at all times, or turned off. Companies have demonstrated surprisingly lack of ethics and security awareness when it comes to cheap consumer hardware:
    - The popular [@internetofshit](https://twitter.com/internetofshit) account on Twitter has various horror stories.
    - Ring (security cameras company, owned by Amazon) has had [security lapses](https://www.geekwire.com/2019/ring-camera-hacks-say-state-security-privacy-technology/)
    - Samsung TVs were found out to be [recording everything you said](https://www.cnet.com/news/samsungs-warning-our-smart-tvs-record-your-living-room-chatter/) and selling that information to third-parties.
    - LG smart TVs were [sending back information on what you watched, list of all files on attached USB drives, and other data](https://www.theguardian.com/technology/2013/nov/21/information-commissioner-investigates-lg-snooping-smart-tv-data-collection) unencrypted to their servers even if you turned off the corresponding setting.
    - Vizio collected viewing histories of 11M users without consent and [had to pay a $2.2M fine](https://www.ftc.gov/news-events/press-releases/2017/02/vizio-pay-22-million-ftc-state-new-jersey-settle-charges-it)

14. If you have to make truly untraceable and secure communications, use [Threema][9], which allows you to signup without a phone number. Signal is great, but you need to give away your phone number to others.

15. If you are uncomfortable sharing your address with cab companies, find a safe location near your home and mark that as your home instead. It could be right across your street.

16. For Facebook, switch to Firefox, and use the [Facebook Container][10].

    >Prevent Facebook from tracking you around the web. The Facebook Container extension for Firefox helps you take control and isolate your web activity from Facebook.

    The same thing also exists for [Twitter][11] and a few other services.

17. I put a limitation on any physical document proofs I submit. Something to the tune of "This is submitted to Airtel on 29-October-2019 for new SIM issuance and is valid for a month" before counter-signing it. I don't know how effective it is though.

18. Learning to assert my Privacy. As Indians, it doesn't come naturally to us. I don't want strangers to photograph me in the crowd, or my face to show up on people's Google Photo suggestions just because I happened to be next to them when they took a selfie. Learning to say no to people who want to photograph you is sometimes harder than you might think. This isn't just speculation - bars and restaurants will photograph you and use your image in their promotional material without asking you.

19. Switching to Firefox is great, especially now that it comes with Privacy Protection enabled by default.

20. For breach notifications, I subscribe to <https://monitor.firefox.com/> which keeps an eye on my email address and notifies me if it has been a part of a breach.


[simpl]: https://getsimpl.com
[mygate]: https://www.mygate.com/

[0]: https://thenextweb.com/google/2017/08/17/how-the-plus-sign-can-save-your-gmail-inbox-from-becoming-a-pit-of-doom/
[1]: https://www.fastmail.com/help/receive/alias-catchall.html
[2]: https://support.apple.com/en-us/HT210318
[3]: https://github.com/gorhill/uBlock/#installation
[4]: https://apps.apple.com/us/app/dnscloak-secure-dns-client/id1452162351
[5]: https://block-this.com/
[6]: https://support.truecaller.com/hc/en-us/articles/212063089-How-do-I-unlist-my-phone-number-
[7]: https://www.truecaller.com/unlisting
[8]: https://www.vulture.com/article/whats-leaving-netflix-movies-shows.html
[9]: https://threema.ch/
[10]: https://addons.mozilla.org/en-US/firefox/addon/facebook-container/
[11]: https://addons.mozilla.org/en-US/firefox/addon/twitter-container/
