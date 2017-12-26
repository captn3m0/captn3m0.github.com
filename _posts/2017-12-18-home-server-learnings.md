---
title: Learnings from building my own home server
layout: post
tags:
- home-server
- arch-linux
- docker
- terraform
- learnings
---

## Learnings

I forgot to do this on the last blog post, so here is the list:

1. archlinux has official packages for [intel-microcode-updates](https://wiki.archlinux.org/index.php/Microcode).
2. wireguard is almost there. I'm running openvpn for now, waiting for the stable release.
3. While [`traefik`][traefik] is great, I'm concerned about the security model it has for connecting to Docker (uses the docker unix socket over a docker mounted volume, which gives it root access on the host). Scary stuff.
4. Docker Labels are a great signalling mechanism. *Update*: After seeing multiple bugs with how `traefik` uses docker labels, they have limited use-cases but work great in those. Don't try to over-architect them for all your metadata.
5. Terraform still needs a lot of work on their docker provider. A lot of updates destroy containers, which should be applied without needing a destroy.
6. I can't proxy gitea's SSH authentication easily, since `traefik` doesn't support TCP proxying yet.
7. The `docker_volume` resource in terraform is useless, since it doesn't give you any control over the volume location on the host. (This might be a docker limitation.)
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

## MongoDB with forceful server restarts

Since my server gets a forceful restart every few days due to power-cuts (I'm still working on a backup power supply), I faced some issues with MongoDB being unable to recover cleanly. The lockfile would indicate a ungraceful shutdown, and it would require manual repairs, which sometimes failed.

As a weird-hacky-fix, since most of the errors were from the MongoDB WiredTiger engine itself, I hypothesized that switching to a more robust engine might save me from these manual repairs. I switched to MongoRocks, and while it has stopped the issue with repairs, the wiki stil doesn't like it, and I'm facing this issue: https://github.com/Requarks/wiki/issues/313

However, I don't have to repair the DB manually, which is a win.

## SSHD on specific Interface

My proxy server has the following 

```
eth0 139.59.22.234
```

And an associated Anchor IP for static IP usecases via Digital Ocean. (`10.47.0.5`, doesn't show up in `ifconfig`).

I wanted to run the following setup:

`eth0:22` -> `sshd`
`Anchor IP:22` -> `simpleproxy` -> `gitea:ssh`

where gitea is the git server hosting `git.captnemo.in`.

Unfortunately, `sshd` doesn't allow you to listen on a specific interface, and since the `eth0` IP is non-static I can't rely on it.

As a result, I've resorted to just using 2 separate ports:

`22` -> `simpleproxy` -> `gitea:ssh`
`222` -> `sshd`

There are some hacky ways around this by creating a new service that boots SSHD after network connectivity, but I thought this was much more stable.

## Wiki.js public pages

I'm using wiki.js setup at <https://wiki.bb8.fun>. A specific requirement I had was public pages, so that I could give links to people for specific resources that could be browser without a login.

However, I wanted the default to be authenticated, and only certain pages to be public. The config for this was surprisingly simple:

### YAML config

You need to ensure that `defaultReadAccess` is false:

```yml
auth:
  defaultReadAccess: false
  local:
    enabled: true
```

### Guest Access

The following configuration is set for the guest user:

![](/img/wiki.js-guest-access.jpg)

Now any pages created under the `/public` directory are now browseable by anyone.

Here is a sample page: <https://wiki.bb8.fun/public/nebula>

## Docker CA Cert Authentication

I wrote a script that goes with the docker TLS guide to help you setup TLS authentication

<script src="https://gist.github.com/captn3m0/2c2e723b2dcd5cdaad733aad12be59a2.js"></script>

## OpenVPN default gateway client side configuration

I'm running a OpenVPN configuration on my proxy server. Howver, I don't always want to use my VPN as the default route, only when I'm in an untrusted network. I still however, want to be able to connect to the VPN and use it to connect to other clients.

The solution is two-fold:

### Server Side

Make sure you *do not* have the following in your OpenVPN `server.conf`:

`push "redirect-gateway def1 bypass-dhcp"`

### Client Side

I created 2 copies of the VPN configuration files. Both of the them have identical config, except for this one line:

`redirect-gateway def1`

If I connect to the VPN config using this configuration, all my traffic is forwarded over the VPN.

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