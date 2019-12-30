---
title: "My Setup: Passwords, 2FA, and security tidbits"
layout: post
---

I upgraded my encryption setup recently, so I thought I should write about it, just in case it is helpful to someone else. As a security professional, I have a different threat model from most folks, and as such my setup does involve a bit more complexity than what I'd recommend to everyone. But if you are a at-risk individual (journalist, person holding hundreds of bitcoins or other digital assets, activist) - you might consider duplicating some of this.

I'll discuss some of the other approaches I've considered, and my thought process around each choice I made.

## Passwords

I used to be on LastPass till 2017[^3], when I migrated to [`pass`][pass] ("the standard unix password manager"). With pass, each password lives inside of a gpg encrypted file whose filename is the title of the website or resource that requires the password. 

`pass` automatically manages a git repository for you, which I sync against GitLab. The one downside of using `pass` is that the list of my domains is visible to my hosting provider. [^1] In the past, I've set this up against Keybase Encrypted Git (Keybase doesn't get to see even the file list), and my own git-server (only I get to see it).

I don't push it to GitHub, since most of my stuff lives on GitHub anyway, and I didn't want to add my passwords there as well. GitLab uptime is decent enough for my usecase (I have [my own git server](https://git.captnemo.in/explore/repos) configured as a fallback if it goes down). Finally, my GitLab account is fairly locked down with:

- zero integrations or third-party apps
- no active personal tokens
- social signin disabled
- only yubikey SSH key configured

### Mobile Passwords

There are 2 primary considerations I have:

1. Using `pass` involves GPG keys, and I can't use hardware GPG keys on my current device (iPhone SE).
2. I don't want to sync all my passwords to my phone. I have a limited number of applications on my device, and syncing all passwords doesn't make sense.

For the first issue, I am forced to use a PGP key in software on [passforios][passforios]. If you are on Android, take a look at [OpenKeychain][okc], and Fidesmo, which both support hardware cards/keys.

For the second issue, I use `pass cp`, and the `.gpg-id` file, which allows me to maintain a `mobile-sync` directory inside my pass git repository encrypted against a different key. From the documentation:

#### `~/.password-store/.gpg-id`

> Contains the default gpg key identification used for encryption and decryption. Multiple gpg keys may be specified in this file, one per line. If this file exists in any sub directories, passwords inside those sub directories are encrypted using those keys. This should be set using the init command.

My `~/.password-store/mobile-sync/.gpg-id` file holds 2 keys: My main encryption key, and the key I've configured on my phone.

Unfortunately, I haven't gotten it working well as a git submodule, so I have a helper script that copies the encrypted password files from `mobile-sync` subdirectory to a different repository (`mobile-passwords.git`). The script is just 2 lines:


```bash
cp -r ~/.password-store/mobile-sync/*.gpg .
git-sync
```

It updates the git repository, and runs a sync to push any local changes to my mobile-passwords repository. I can pull that on my passforios application.

## GPG

`pass` relies on GPG, and as such I require a strong key setup. I have the following:


1. 2xYubikey 4 (Doesn't have NFC)
2. SoloKey (Only supports U2F)[^2]
3. Fidesmo Smartcard, currently unused

Both the Yubikeys are configured against my GPG Encryption key. I carry one of the Yubikeys and the Solokey on my keyring with me. The backup Yubikey stays at my home.

I followed [this guide](https://github.com/drduh/YubiKey-Guide#multiple-keys) while configuring the same. As of now, switching between keys is not very user-friendly, but future [GnuPG versions plan to fix it](https://dev.gnupg.org/T2291). The Yubikey holds:

- An encryption key
- A signing key
- An authentication key

The master key is backed up using [paperkey](https://wiki.archlinux.org/index.php/Paperkey) and a strong password. I have a subkey backup as well, since Yubikeys are known to fail (I lost my previous GPG key because my Yubikey stopped working).

## SSH

The Authentication key in my Yubikey is configured for SSH. I just need to ensure that my GPG agent is configured for SSH as well:

```bash
export GPG_TTY="$(tty)"
export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
gpgconf --launch gpg-agent
```

## U2F

U2F lets me use a physical key as my second-factor on supported websites. I configure all 3 (2xYubikey+Solokey) of my keys for U2F wherever possible. Lots of websites (AWS/Twitter for eg) don't support multiple U2F keys, and I use the Yubikey in such places.

## Root-of-Identity

For most people, the root of your identity comes down to ownership of your email. As such, it is very often the juiciest target for most attackers. I run my mail against [Migadu](https://www.migadu.com), a privacy friendly swiss email-hosting service. They provide me a management layer for managing my domains which uses my GMail account. (See FAQ for why). I also have 2FA (TOTP only) configured on the Migadu management setup.

The domain is currently registered at a Indian registrar (which doesn't offer U2F, but I do have TOTP configured). I would have moved this to CloudFlare, but CloudFlare doesn't support the `.in` TLD yet.[^6]

The email address used for registring the domain again is my GMail.

## Recovery/Backup codes and Security Questions

I use randomly generated UUIDs as answers to security questions. Currently, I'm storing these for various services within the same password store. As it stands, I can't get access to my password OR recovery token without my Yubikey and PIN. The access Matrix looks like this:

|What|Physical Access|Additional Authentication|
|---|---|---|
|Password|Yubikey|PIN|
|U2F-2FA|Yubikey OR SoloKey|Physical touch|
|TOTP|Phone|TouchID|
|Recovery Code|Yubikey|PIN|
|Security Question answers|Yubikey|PIN|

## Failure Scenarios

There are lots of failure scenarios with such a setup, and while I've got a pretty spotless record of not being hacked - I'm not immune to screwups. Here's all the bad things that can happen:

### Yubikey failures

If my Yubikey fails (or if I forget its PIN), I can't access passwords on my device. My backup Yubikey is kept safely at home.

### Device failures

I have a current version of the password repository against 3 PCs, and a partial version in my mobile. If all these 4 devices fail at once, I can still clone a fresh version of the repository with my YubiKey (I would still have GitLab SSH access). I might need to prepare better for this though, since configuring GPG-SSH might not always be easy during an incident.

### Circular dependency against GitLab

My GitLab password is randomly generated and stored on the same password store. That is not too big of an issue, because I don't need the GitLab password anymore to clone my passwords repo, just my Yubikey (for SSH).

### Lost Key

If I lose my key, the GPG card contains public info, including my email address, which can be used to contact me. I have a Tile bluetooth tracker on my keychain to make it easier for me to find it.

## Improvements

If you have any suggestions for any of the below, I'm happy to hear them.

### Travel Plans

Since my backup key stays at home, how do I deal with long-term travel? This is something I'm still figuring out. Do I take my backup Yubikey on my longer-travels? Or should I setup a third-key before I do that? Chances of me losing both the keys together are quite high, so I'm trying to avoid that.

### Domain Ownership

I'd like to transfer my domain to one of these 4 registrars that support U2F:

- Gandi
- NameCheap
- Porkbun
- Google Domains

I already own some domains with uncommon TLDs, mostly via Namecheap[^5]

If you use CloudFlare, they should roll out [U2F support soon](https://community.cloudflare.com/t/u2f-for-logins/17583/34).

### 2FA Recovery Guides

I wish more organizations published what they consider as valid 2FA recovery mechanisms. GitHub supports 2FA recovery by proof of SSH keys or Personal Tokens; Migadu just needs a few domain names from your account, and lots of services require proof-of-identity.

A lot of this is undocumented, and I wish organizations were more public about this so users can take appropriate measures and understand their risk better.

### Fidesmo Card

I'm planning to configure my Fidesmo card against my existing GPG/SSH key, so it stays in my wallet to improve redundancy. Unfortunately, it is not supported on iOS, so I plan to get a NFC reader/writer and test that out. This also helps with travel plans a bit, since I'm less likely to lose my wallet (which also has a bluetooth tracker).

### U2F on iPhone

U2F support on Mobile Safari is non-existent. Brave recently added support for the upcoming Yubikey 5Ci, which supports both USB-C and lightning. However, this requires a special Yubikey SDK, which breaks the idea of U2F being interoperable. The 5Ci is also quite costly at $70. I don't know of any application that is actually supporting GPG-over-Yubikey-over-lightning.

Compare this to Android where NFC based smartcards or Yubikeys just work. I'd like that to happen with iPhones.


### Full Disk Encryption using a Yubikey

It is possible to configure [Full Disk Encryption with Yubikeys](https://github.com/agherzan/yubikey-full-disk-encryption), but I haven't tried it yet.

### 2FA on my email account

Migadu currently _does not support 2FA on webmail access_, just on `manage.migadu.com`. This is very unfortunate, but I'm told this is planned soon (January 2020).

### Recovery/Backup codes and Security Questions

My current setup of saving recovery codes alongside passwords isn't optimal, but I don't have a better way either. I've considered keeping my recovery codes on a alternate password store (such as bitwarden, or keypassX), but I'll have to memorize the password, and setup a separate 2FA for it to be truly fault-tolerant.

## FAQ

### Why do you have stuff configured on your GMail? Aren't you anti-Google?

Despite all the flak that Google gets for privacy, their security team is pretty awesome. Your account is pretty much unhackable once you are enrolled into their Advanced Protection Program. The only two security-sensitive places where I use it are:

1. Domain Registration
2. Email Management

Everywhere else, I use my actual domain (captnemo.in) to ensure nothing else routes over GMail. Using GMail for the above 2 ensures that I don't have a circular dependency. If I were to lose my main email password, I can recover via multiple ways:

1. Change DNS to another email provider.
2. Reset password via migadu admin panel.

Ensuring that either of these workflows do not rely on the same email account I've just lost access to is vital. Another alternative is to use a trusted-friend as a proxy for these emails, and use their domain for managing these 2 services. Might get around to it someday.

### What do you recommend I use?

- [Bitwarden](https://bitwarden.com/) for password management.
- 2x[HyperFIDO Mini U2F](https://www.amazon.in/HyperFIDO-Mini-U2F-Security-Key/dp/B01LZO0WE9) Keys configured [against as many accounts as possible](https://www.dongleauth.info/). U2F is not only safer, but much more convenient than TOTP/SMS based 2FA. For iPhone/USB-C users, see [the Yubico website](https://www.yubico.com/products/compare-yubikey-5-series/).
- If you'd like to get off GMail, pay for FastMail. Alternatively, if I know you in real-life, I'm happy to host your mail in my Migadu account. (Only works if you know me well enough to trust me)
- A PIN configured on all your SIMs.
- Full-Disk-Encryption on all your devices
- Get a SIM without an Aadhaar, to make SIM-Jacking attackes harder (applies in India).
- Use randomly generated passwords everywhere.
- Setup a PIN on your WhatsApp
- If you own a lot of cryptocurrency, use a hardware wallet and put it in a bank safe. And have a backup one, in another safe. You can put the PIN for those in your password store. I haven't researched enough to suggest you which wallet.

### Why are you so paranoid?

I work in infosec. Breaking things comes naturally to me, and I plan for defense-in-depth. Plus, I'd be a terrible security guy if I got hacked.


[^1]: The [pass-tomb](https://github.com/roddhjav/pass-tomb) extension bypasses this limit and encrypts your filenames as well.
[^2]: The Solokey is mostly redundant in this setup, but I have it around because I have it configured in a few places where the Yubikey isn't. I'm slowly phasing it out.
[^3]: I moved away from Lastpass after Tavis Ormandy reported a RCE vulnerability on their browser extension. Their wikipedia page mentions 2 breaches, and 3 security incidents. It has never undergone a security audit (unlike bitwarden) and is not something I recommend anymore.
[^5]: Namecheap announced [U2F support](https://www.namecheap.com/blog/protect-account-totp-2-factor/) in April 2019, and while it was buggy at first, it has definitely improved.
[^6]: The domain is stuck in a legal limbo, because of an [ongoing case between my registrar and NIXI](https://our.in/mitsu-ceo-got-upset-with-the-nixi-proceedings/) (which runs the `.in` registry).

[passforios]: https://mssun.github.io/passforios/
[okc]: https://www.openkeychain.org/
[pass]: https://passwordstore.org