---
title: Home Server Networking
layout: post
image: networking.jpg
tags: 
    - home-server
    - Networking
    - VPN
    - ACT
---

Next in the Home Server series, this post documents how I got the networking setup to
serve content publicly from my under-the-tv server.

![Colorful block diagram for the networking setup](/img/networking.jpg)

## Background

My home server runs on a mix of Docker/Traefik orchestrated via Terraform. The source code is
at <https://git.captnemo.in/nemo/nebula> (self-hosted, dogfooding FTW!) if you wanna take a look.

The ISP is ACT Bangalore[^1]. They offer decent bandwidth and I've been a customer long time.

## Public Static IP

In order to host content, you need a stable public IP. Unfortunately, ACT puts all of its customers
in Bangalore behind a NAT [^2]. As a result, I decided to get a [Floating IP from Digital Ocean][fip] [^3].

The Static IP is attached to a cheap Digital Ocean Droplet (10$/mo). If you resolve `bb8.fun`, this is the IP you will get:

```
Name:   bb8.fun
Address: 139.59.48.222
```

The droplet has a public static IP of it's own as well: `139.59.22.234`. The reason I picked a Floating IP is because DO gives them for free, and I can switch between instances later without worrying about it.

## Floating IP

On the Digital Ocean infrastructure side, this IP is not directly attached to an interface on your droplet. Instead,
DO uses something called "Anchor IP":

>Network traffic between a Floating IP and a Droplet flows through an anchor IP, which is an IP address aliased to the Droplet's public network interface (eth0). You should bind any public services that you want to make highly available through a Floating IP to the anchor IP.

So, now my Droplet has 2 different IPs that I can use:

1. Droplet Public IP (`139.59.22.234`), assigned directly to the `eth0` interface.
2. Droplet Anchor IP (`10.47.0.5`), setup as an alias to the `eth0` interface.

This doubles the number of services I can listen to. I could have (for eg) - 2 different webservers
on both of these IPs.

## OpenVPN

In order to establish NAT-punching connectivity between the Droplet and the Home Server, I run OpenVPN server
on the Droplet and `openvpn-client` on the homeserver.[^4]

The [Digital Ocean Guide][openvpnguide] is a great resource if you ever have to do this. 2 specific IPs on the OpenVPN
network are marked as static:

1. Droplet: `10.8.0.1`
2. Home Server: `10.8.0.14`

## Home Server - Networking

- The server has a private static IP assigned to its `eth0` interface
- It also has a private static IP assiged to its `tun0` interface

There are primarily 3 kinds of services that I like to run:

1. Accessible only from within the home network (Timemachine backups, for eg) (Internal). This I publish on the `eth0` interface.
2. Accessible only from the public internet (Wiki) (Strictly Public). These I publish on the `tun0` interface and proxy via the droplet.
3. Accessible from both places (Emby, AirSonic) (Public). These I pubish on both `tun0` and the `eth0` interface on the homeserver.

## Docker Networking Basics

Docker runs its own internal network for services, and lets you "publish" these services
by forwarding traffic from a given interface to them.

In plain docker-cli, this would be:

`docker run nginx --publish 443:443,80:80` (forward traffic on 443,80 on all interfaces to the container)

Since I use Terraform, it looks [like the following for Traefik](https://git.captnemo.in/nemo/nebula/src/branch/master/docker/traefik.tf):

{%comment%} This is HCL, but rogue doesn't support it, so fake it by perl{%endcomment%}
```perl
# Admin Backend
ports {
  internal = 1111
  external = 1111
  ip       = "${var.ips["eth0"]}"
}

ports {
  internal = 1111
  external = 1111
  ip       = "${var.ips["tun0"]}"
}

# Local Web Server
ports {
  internal = 80
  external = 80
  ip       = "${var.ips["eth0"]}"
}

# Local Web Server (HTTPS)
ports {
  internal = 443
  external = 443
  ip       = "${var.ips["eth0"]}"
}

# Proxied via sydney.captnemo.in
ports {
  internal = 443
  external = 443
  ip       = "${var.ips["tun0"]}"
}

ports {
  internal = 80
  external = 80
  ip       = "${var.ips["tun0"]}"
}
```

There are 3 "services" exposed by Traefik on 3 ports:

Traefik Admin Interface
: Useful for debugging. I leave this in Read-Only mode with no authentication. This is an *Internal* service

HTTP, Port 80
: This redirects users to the next entrypoint (HTTPS). This is a *Public* service.

HTTPS, Port 443
: This is where most of the traefik flows. This is a *Public* service.

For all 3 of the above, Docker forwards traffic from both OpenVPN, as well as the home network. OpenVPN lets me access this from my laptop when I'm not at home, which is helpful for debugging issues. However, to keep the Admin Interface internal, it is not published to the internet.

# Internet Access

The "bridge" between the Floating IP and the OpenVPN IP (both on the Digital Ocean droplet) is `simpleproxy`. It is a [barely-maintained 200 line TCP-proxy](https://github.com/vzaliva/simpleproxy). I picked it up because of its ease of use as a TCP Proxy. I specifically looked for a TCP Proxy because:

1. I did not want to terminate SSL on Digital Ocean, since Traefik was already doing LetsEncrypt cert management for me
2. I also wanted to proxy non-web services (more below).

The simpleproxy configuration consists of a few systemd units:

```ini
[Service]
Type=simple
WorkingDirectory=/tmp
# Forward Anchor IP 80 -> Home Server VPN 80
ExecStart=/usr/bin/simpleproxy -L 10.47.0.5:80 -R 10.8.0.14:80
Restart=on-abort

[Install]
WantedBy=multi-user.target

[Unit]
Description=Simple Proxy
After=network.target
```

I run 3 of these: 2 for HTTP/HTTPS, and another one for SSH.

# SSH Tunelling

When I'm on the go, there are 3 different SSH services I might need:

1. Digital Ocean Droplet
2. Home Server
3. Git (`gitea` runs its own internal git server)

My initial plan was:

1. Forward Port 22 Floating IP Traffic to Gitea.
2. Use the `eth0` interface on the droplet to run the droplet `sshd` service.
3. Keep the Home Server SSH forwarded to OpenVPN, so I can access it over the VPN network.

Unfortunately, that didn't work out well, because `sshd` [doesn't support listening on an Interface](https://serverfault.com/questions/605446/make-sshd-listen-to-a-specific-interface). I could have used the Public Droplet IP, but I didn't like the idea.

The current setup instead involves:

1. Running the droplet `sshd` on a separate port entirely (2222).
2. The `simpleproxy` service forwarding port 22 traefik to 2222 on OpenVPN IP which is then published by Docker to the `gitea` container's port 22.

[The complete traefik configuration](https://git.captnemo.in/nemo/nebula/src/branch/master/docker/conf/traefik.toml) is also available if you wanna look at the entrypoints in detail.

# Caveats

## Traefik Public Access

You might have noticed that because `traefik` is listening on both `eth0` and `tun0`, there is no guarantee of a "strictly internal" service via Traefik. Traefik just uses the Host headers in the request (or SNI) to determine the container to which it needs to forward the request. I use `*.in.bb8.fun` for internaly accessible services, and `*.bb8.fun` for public. But if someone decides to spoof the headers, they can access the Internal service.

Since I'm aware of the risk, I do not publish anything via traefik that I'm not comfortable putting on the internet. Only a couple of services are marked as "internal-also", and are published on both. Services like Prometheus are not published via Traefik.

## 2 Servers

Running and managing 2 servers takes a bit more effort, and has more moving parts.
But I use the droplet for other tasks as well (running my [DNSCrypt Server][dnscrypt], for eg).

## Original IP Address

Since SimpleProxy does not support the [Proxy Protocol](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt),
both Traefik and Gitea/SSH servers don't get informed about the original IP Address. I plan to fix that by switching to HAProxy TCP-mode.

{% include selfhosted.md %}

[^1]: If you get lucky with their customer support, some of the folks I know have a static public IP on their home setup. In my case, they asked me to upgrade to a corporate plan.
[^2]: I once scanned their entire network using `masscan`. It was fun: <https://medium.com/@captn3m0/i-scanned-all-of-act-bangalore-customers-and-the-results-arent-surprising-fecf9d7fe775>
[^3]: AWS calls its "permanent" IP addresses "Elastic" and Digital Ocean calls them "Floating". We really need better names in this industry.
[^4]: Migrating to Wireguard is on my list, but I haven't found any good documentation on running a hub-spoke network so far.

[fip]: https://www.digitalocean.com/community/tutorials/how-to-use-floating-ips-on-digitalocean
[openvpnguide]: https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-16-04 "by Justin Ellingwood"
[dnscrypt]: https://captnemo.in/dnscrypt/