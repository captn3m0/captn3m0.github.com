---
layout: post
title: Migrating from Google (and more)
tags:
    - selfhosted
    - migration
    - google
---

<div class="toc" markdown="1">
#### Contents

- [Email](#email)
- [Google Play Music](#google-play-music)
- [Google Keep](#google-keep)
- [Phone](#phone)
  * [microG Core](#microg-core)
  * [UnifiedLP](#unifiedlp)
  * [Maps](#maps)
  * [Uber](#uber)
  * [Calendar/Contacts](#calendar-contacts)
  * [Google Play Store](#google-play-store)
- [LastPass](#lastpass)
- [GitHub](#github)
</div>

As part of working on my home-server setup, I wanted to move off few online services to ones that I manage. This is a list of what all services I used and what I've migrated to .

_Why_: I got frustrated with [Google Play Music][gpm] a few times. Synced songs would not show up across all clients immediately (I had to refresh,uninstall,reinstall), and I hated the client limits it would impose. Decided to try [microG][mg] on my phone at the same time, and it slowly came together.

# Email

I've been using email on my own domain for quite some time (`captnemo.in`), but it was managed by a Outlook+Google combination that I didn't like very much.

I switched to [Migadu][migadu] sometime last year, and have been quite happy with the service. Their [Privacy Policy](https://www.migadu.com/privacy/), and [pro/cons](https://www.migadu.com/procon/) section on the website is a pleasure to read.

_Why_: Email is the central-point of your online digital identity. Use your own-domain, at the very least. That way, you're atleast protected if Google decides to suspend your account. Self-hosting email is a big responsibility that requires critical uptime, and I didn't want to manage that, so went with migadu.

_Why Migadu_: You should read their [HN thread](https://news.ycombinator.com/item?id=13048334).

_Caviats_: They don't yet offer 2FA, but hopefully that should be fixed soon. Their spam filters aren't the best either. Migadu even has a [Drawbacks](https://www.migadu.com/procon/#the-drawbacks-list) section on their website that you _must read_ before signing up.

_Alternatives_: RiseUp, FastMail.

# Google Play Music

I quite liked [Google Play Music][gpm]. While their subscription offering is horrible in India, I was a happy user of their "bring-your-own-music" plan. In fact, the most used Google service on my phone happened to be Google Play Music! I switched to a nice subsonic fork called [AirSonic][airsonic], which gives me the ability to:

- Listen on as many devices as I want (Google has some limits)
- Listen using multiple clients at the same time
- Stream at whatever bandwidth I pick (I stream at 64kbps over 2G networks!)

I'm currently using [Clementine](https://www.clementine-player.org/) on the Desktop (which unfortunately, doesn't cache music), and [UltraSonic](https://github.com/ultrasonic/ultrasonic/) on the phone. Airsonic even supports bookmarks, so listening to audiobooks becomes much more simpler.

_Why_: I didn't like Google Play Music limits, plus I wanted to try the "phone-without-google" experiment.

_Why AirSonic_: [Subsonic](https://github.com/sindremehus/subsonic) is now closed source, and the [Libresonic developers forked off to AirSonic](https://www.reddit.com/r/selfhosted/comments/6saiac/airsonic_is_out/dlbea94/), which is under active development. It is supports across all devices that I use, while [Ampache][ampache] has spotty Android support.

# Google Keep

I switched across to [WorkFlowy](https://workflowy.com), which has both a Android and a Linux app (both based on webviews). I've used it for years, and it is a great tool. Moreover, I'm also using DAVDroid sync for Open Tasks app on my phone. Both of these work well enough offline.

_Why_: I didn't use Keep much, and WorkFlowy is a far better tool anyway.

_Why WorkFlowy_: It is _the best_ note-taking/list tool I've used.

# Phone

I switched over to the [microG fork of lineageOS](https://lineage.microg.org/) which offers a reverse-engineered implementation of the Google Play Services modules. It includes:

## microG Core

Which talks to Google for Sync, Account purposes.

_Why_: Saves me a lot of battery. I can uninstall this, unlike Google Play Services.

_Cons_: Not all google services are supported very well. Push notifications have some issues on my phone. See the [Wiki](https://github.com/microg/android_packages_apps_GmsCore/wiki/Implementation-Status) for Implementation Status.

## UnifiedLP

Instead of the Google Location Provider. I use the Mozilla Location Services, along with Mozilla Stumbler to help improve their data.

_Why_: Google doesn't need to know where I am.

_Caviats_: GALP (Google Assisted Location Provider) does GPS locks much faster in comparision. However, I've found the Mozilla Location Services coverage in Bangalore to be pretty good.

## Maps

Stil looking for decent alternatives.

## Uber

microG comes with a Google Maps shim that talks to Open Street Maps. The maps feature on Uber worked fine with that shim, however booking cabs was not always possible. I switched over to `m.uber.com` which worked quite well for some time.

Uber doesn't really spend resources on their mobile site though, and it would ocassionaly stop working. Especially with regards to payments. I've switched over to the Ola mobile website, which works pretty well. I keep the OlaMoney app for recharging the OlaMoney wallet alongside.

Uber->Ola switch was also partially motivated by [how-badly-run Uber is](https://www.theguardian.com/technology/2017/jun/18/uber-travis-kalanick-scandal-pr-disaster-timeline).

## Calendar/Contacts

Most implementations support caldav/carddav for calendar/contacts sync. I'm using DAVDroid for syncing to a self-hosted [Radicale Server][radicale].

_Why_: I've always had contacts synced to Google, so it was always my-single-source-of-truth for contacts. But since I'm on a different email provider now, it makes sense to move off those contacts as well. Radicale also lets me manage multiple addressbooks very easily.

_Why Radicale_: I looked [around at alternatives](https://github.com/Kickball/awesome-selfhosted#calendaring-and-contacts-management), and 2 looked promising: Sabre.io, and Radicale. Sabre is no longer under development, so I picked Radicale, which also happened to have a [regularly updated docker image](https://hub.docker.com/r/tomsquest/docker-radicale/).

## Google Play Store

Switch to [FDroid](https://f-droid.org/) - It has some apps that [Google doesn't](https://adaway.org/) [like](https://newpipe.schabi.org/), and some more. Moreover, you can use YALP Store to download any applications from the Play Store. You can even run a FDroid repository for the apps you use from Play Store, as an alternative. See [this excellent](https://shadow53.com/android/no-gapps/faq/can-i-use-the-official-play-store-with-microg/) guide on the various options.

_Why_: Play Store is tightly linked to Google Play Services, and doesn't play nice with [microG][mg].

_Why FDroid_: FDroid has [publicly verifiable builds](https://f-droid.org/docs/Reproducible_Builds/?title=Deterministic,_Reproducible_Builds), and tons of open-source applications.

_Why Yalp_: Was easy enough to setup.

If you're looking to migrate to MicroG, I'd recommend going through the entire [NO Gapps Setup Guide](https://shadow53.com/android/no-gapps/setup-guide/microg/) by shadow53 before proceeding.

# LastPass

I've switched to `pass` along with a sync to keybase.

_Why_: [LastPass has had multiple breaches](https://en.wikipedia.org/wiki/LastPass#Security_issues), and a plethora of security issues (including 2 RCE vulnerabilities). Their fingerprint authentication on Android could be bypassed til recently. _I just can't trust them any more_

_Why pass_: It is built on strong crypto primitives, is open-source, and has good integration with both [`i3`](https://github.com/cdown/passmenu) and [firefox](https://github.com/browserpass/browserpass-extension). There is also a [LastPass migration script](https://git.zx2c4.com/password-store/tree/contrib/importers/lastpass2pass.rb) that I used.

_Caviats_: Website names are used as filenames in pass, so even though passwords are encrypted, you don't want to push it to a public Git server (since that would expose the list of services you are using). I'm using my [own git server][git], along with keybase git(which keeps it end-to-end encrypted, even branch names). You also need to be careful about your GPG keys, instead of a single master password.

# GitHub

For bonus, I setup a Gitea server hosted at [git.captnemo.in][git]. [Gitea][gitea] is a fork of [gogs][gogs], and is a single-binary go application that you can run easiy.

Just running it for fun, since I'm pretty happy with my GitHub setup. However, I might move some of my sensitive repos (such as [this][dirlink]) to my own host.

_Why Gitea_: The other alternatives were `gogs`, and GitLab. There have been concerns about gogs development model, and GitLab was just too overpowered/heavy for my use case. (I'm using the home server for gaming as well, so it matters)

{% include selfhosted.md %}

[gpm]: https://music.google.com "Google Play Music"
[mg]: https://microg.org/ "MicroG is a free-as-in-freedom re-implementation of Google’s proprietary Android user space apps and libraries."
[migadu]: http://www.migadu.com/ "Migadu is email hosting built and operated by humans"
[radicale]: https://radicale.org "A Free and Open-Source CalDAV and CardDAV Server, runs on Python"
[git]: https://git.captnemo.in "Hosted by gitea, uptime not guaranteed"
[gitea]: https://gitea.io/en-US/
[gogs]: https://gogs.io/
[dirlink]: https://github.com/captn3m0/dir-600l "Reverse engineered firmware for my D-Link 600L router"
[nebula]: https://git.captnemo.in/nemo/nebula "If this is down, wait"
[ampache]: http://ampache.org/