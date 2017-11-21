---
title: Running terraform and docker on my home server
layout: post
tags:
- home-server
- arch-linux
- docker
- terraform
---

The last time I'd posted about my Home Server build in September, I'd just gotten it working. Since then, I've made a lot of progress. It is now running almost 10 services, up from just Kodi back then. Now it has a working copy of:

[Kodi][kodi]
: I was running `kodi-standalone-service`, set to run on boot, as per the [ArchLinux Wiki][kodi-wiki-standalone], but switched in favor of openbox to a simple autorun.

[Steam][steam]
: The current setup uses Steam as the application launcher. This lets me ensure that the Steam Controller works across all applications.

[Openbox][openbox]
: Instead of running Kodi on xinit, I'm now running openbox with autologin against a non-privileged user.

PulseAudio
: I tried fighting it, but it was slightly easier to configure compared to dmix. Might move to dmix if I get time.

btrfs
: I now have the following disks:
1. 128GB root volume. (Samsung EVO-850)
2. 1TB volume for data backups
3. 3TB RAID0 configuration across 2 disks.
There are some btrfs subvolumes in the 3TB raid setup, including one specifically for docker volumes. The docker guide recommends running btrfs subvolumes on the block device, which I didn't like, so I'm running docker volumes in normal mode on a btrfs disk. I don't have enough writes to care much yet, but might explore this further.

[Docker][docker]
: This has been an interesting experiment. Kodi is still installed natively, but I've been trying to run almost everything else as a docker container. I've managed to do the configuration entirely via terraform, which has been a great learning experience. I've found terraform much more saner as a configuration system compared to something like ansible, which gets quite crazy. (We have a much more crazy terraform config at work, though).

[Terraform][tf]
: I have a private repository on GitLab called `nebula` which I use as the source of truth for the configuration. It doesn't hold everything yet, just the following:
1. Docker Configuration (not the docker service, just the container/volumes)
2. CloudFlare - I'm using `bb8.fun` as the root domain, which is entirely managed using the CloudFlare terraform provider.
3. MySQL - Running a MariaDB container, which has been configured by-hand till [this PR gets merged][pr].

[Gitea][gitea]
: Running as a docker container, provisioned using terraform. Plan to proxy this using `git.captnemo.in`.

[Emby][emby]
: Docker Container. Nothing special. Plan to set this up as the Kodi backend.

[Couchpotato][couchpotato]
: Experimental setup for now. Inside a docker container.

[Flexget][flexget]
: I wish I knew how to configure this. Also inside docker.

[traefik][traefik]
: Running as a simple reverse proxy for most of the above services

[elibsrv][elibsrv]
: A simple OPDS server, which I use against my Kindle. If you don't know what OPDS is, you should [check this out][]. Running on a simple apache setup on the archlinux box for now. WIP for dockerization.

[ubooquity][ubooquity]
: Simple ebook server. Proxied over the internet. Has a online ebook reader, which is pretty cool.

MariaDB
: I set this up planning to shift Kodi's data to this, but now that I have emby setup - I'm not so sure. Still, keeping this running for now.

[Transmission][transmission]
: Hooked up to couchpotato,flexget, and sickrage so it can do things.

[Sickrage][sickrage]
: Liking this more than flexget so far, much more easier to configure and use.

[AirSonic][airsonic]
: This is the latest fork of libresonic, which was itself forked off subsonic. My attempt at getting off Google Play Music.

## Learnings

I forgot to do this on the last blog post, so here is the list:

1. archlinux has official packages for [intel-microcode-updates](https://wiki.archlinux.org/index.php/Microcode).
2. wireguard is almost there. I'm running openvpn for now, waiting for the stable release.
3. While [`traefik`][traefik] is great, I'm concerned about the security model it has for connecting to Docker (uses the docker unix socket over a docker mounted volume, which gives it root access on the host). Scary stuff.
4. Docker Labels are a great signalling mechanism.
5. Terraform still needs a lot of work on their docker provider. A lot of updates destroy containers, which should be applied without needing a destroy.
6. I can't proxy gitea's SSH authentication easily, since `traefik` doesn't support TCP proxying yet.
7. The `docker_volume` resource in terraform is useless, since it doesn't give you any control over the volume location on the host.
8. The `upload` block inside a `docker_container` resource is a great idea. Lets you push configuration straight inside a container. This is how I push configuration straight inside the `traefik` container for eg:
  ```hcl
upload {
  content = "${file("${path.module}/conf/traefik.toml")}"
  file    = "/etc/traefik/traefik.toml"
}
```

## Advice

This section is if you're venturing into a docker-heavy terraform setup:

1. Use `traefik`. Will save you a lot of pain with proxying requests.
2. Repeat the `ports` section for every IP you want to listen on. CIDRs don't work.
3. If you want to run the container on boot, you want the following:
    ```ini
    restart = "unless-stopped"
    destroy_grace_seconds = 10
    must_run = true
    ```
4. If you have a single `docker_registry_image` resource in your state, you can't run terraform without internet access.
5. Breaking your docker module into `images.tf`, `volumes.tf`, and `data.tf` (for registry_images) works quite well.
6. Memory limits on docker containers can be too contrained. Keep an eye on logs to see if anything is getting killed.
7. Setup Docker TLS auth _first_. I tried proxying Docker over apache with basic auth, but it didn't work out well.

When I'd started the project, I'd looked at GUI based docker management solutions (Portainer, Shipyard, Rancher), but I've found that the tough parts for me (container linking, ports, environments, volumes) were all handled much more cleanly by just terraform.

## TODO

A few things off my TODO list:

1. Create a Docker image for elibsrv that comes with both `ebook-convert` and `kindlegen` pre-installed
2. Do the same for ubooquity as well

[kodi-wiki-standalone]: https://wiki.archlinux.org/index.php/Kodi#Kodi-standalone-service
[pr]: https://github.com/hashicorp/go-version/pull/34
[sickrage]: https://sickrage.github.io/
[transmission]: https://transmissionbt.com/
[kodi]: https://kodi.tv/
[steam]: http://store.steampowered.com/linux
[openbox]: http://openbox.org/wiki/Main_Page
[docker]: https://www.docker.com/
[tf]: https://www.terraform.io/
[gitea]: https://github.com/go-gitea/gitea
[emby]: https://emby.media/
[couchpotato]: https://couchpota.to/
[flexget]: https://flexget.com/
[traefik]: https://traefik.io/
[elibsrv]: http://elibsrv.sourceforge.net/
[ubooquity]: https://vaemendis.net/ubooquity/
[airsonic]: https://airsonic.github.io/