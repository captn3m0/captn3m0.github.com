---
layout: post
title: Migrating DNSCrypt Server to Docker
---

I've been running a personal [DNSCrypt server in Bangalore][doc] for the last 2 years. When I set it up, it was just a compiled version of `dnscrypt-wrapper`, which was the bare minimum setup I could do.

Since then, I've upgraded it to a distribution supported version, but recent changes in [dnscrypt key rotation](https://dnscrypt.pl/2017/01/04/keys-are-now-rotated-every-24-hours/), I've been wanting to setup something automated as well.

The easiest way was to switch to the official [DNSCrypt Docker](https://github.com/DNSCrypt/dnscrypt-server-docker) image, which does both key generation and certificate rotation. Since my public key was already present in the [DNSCrypt Server lists][lists], I was not too keen to regenerate a new key.

The primary challenge was ensuring that the docker container picks up my existing keys without trying to generate new ones from scratch. It was basically 2 steps:

1.  Match the directory structure that the container expects.
2.  Invoke the container directly into `start` mode while passing existing keys.

## Directory Structure

I copied my keys (`public.key`, `secret.key`) to `/etc/dnscrypt-keys` and ran the following:

```
echo 2.dnscrypt-cert.captnemo.in > provider_name
touch provider_info.txt # I couldn't figure out how to output the same info, so kept it blank
hexdump -ve '1/1 "%.2x"' < public.key > public.key.txt
```

Then I ensured that the file permissions are matching what the container expects:

```
chmod 640 secret.key
chmod 644 public.key
chown root:1002 public.key secret.key
chmod 644 provider_name
```

This is how the final permissions looked for the directory (`/etc/dnscrypt-keys`)

```
-rw-r-----   1 root 1002    64 May 18 07:15 secret.key
-rw-r--r--   1 root 1002    32 May 18 07:15 public.key
-rw-r--r--   1 root root    28 May 18 07:19 provider_name
-rw-r--r--   1 root root     0 May 18 07:23 provider_info.txt
-rw-r--r--   1 root root    64 May 18 07:25 public.key.txt
drwxr-xr-x   2 root root  4096 May 18 07:26 .
```

## Running the Container

Then, I directly ran `dnscrypt-wrapper` container:

```
docker run --detatched --restart=unless-stopped --volume /etc/dnscrypt-keys:/opt/dnscrypt-wrapper/etc/keys --publish 10.47.0.5:4434:443/tcp --publish 10.47.0.5:4434:443/udp jedisct1/dnscrypt-server start
```

I pass a host path mount instead of creating a Docker Volume, since they can get deleted in regular `docker prune`.

Here, `10.47.0.5` is the ["Anchor IP"][anchor], which Digital Ocean internally maps to my [Floating IP][fip].

The container comes up, generates new short-term keys and goes live:

```
Starting DNSCrypt service for provider:
2.dnscrypt-cert.captnemo.in
Starting pre-service scripts in /etc/runit_init.d
setup in directory /opt/unbound/etc/unbound
generating unbound_server.key
Generating RSA private key, 3072 bit long modulus (2 primes)
.......++++
...................++++
e is 65537 (0x010001)
generating unbound_control.key
Generating RSA private key, 3072 bit long modulus (2 primes)
.........................++++
........................................++++
e is 65537 (0x010001)
create unbound_server.pem (self signed certificate)
create unbound_control.pem (signed client certificate)
Signature ok
subject=CN = unbound-control
Getting CA Private Key
Setup success. Certificates created. Enable in unbound.conf file to use
ok: run: unbound: (pid 28) 300s
ok: run: dnscrypt-wrapper: (pid 31) 300s
ok: run: unbound: (pid 28) 600s
ok: run: dnscrypt-wrapper: (pid 31) 600s
```

Once the server was up, I verified connectivity with `dnscrypt-proxy` and it worked perfectly.

[doc]: https://captnemo.in/dnscrypt/
[lists]: https://dnscrypt.info/public-servers
[anchor]: https://www.digitalocean.com/docs/networking/floating-ips/how-to/find-anchor-ips/
[fip]: https://www.digitalocean.com/docs/networking/floating-ips/
