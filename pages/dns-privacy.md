---
title: DNS Privacy Policy
layout: page
permalink: /dns/privacy/
---

This policy covers applies to the following services (called `resolver`):

1.  [DNSCrypt Resolver](/dnscrypt/)
2.  [DoH Resolver](/doh/)

The policy aims to be compliant with [Mozilla's Trusted Recursive Resolver (TRR) program][trr].

## CHANGELOG

| Date       | Change                      |
| :--------- | :-------------------------- |
| 2019-05-12 | Draft Version published     |
| 2019-05-28 | Second Draft [see diff][v2] |

## tl;dr

Your data is not logged by default. If it has to be logged, it will be deleted within 1 hour. No queries or respones are modified, and no domains are blocked or filtered. If law enforcement forces me to do anything of the above, the [block list](/dns/blocked.txt) will be updated, along with an Annual Transparency Report. Your data (even anonymized or aggregate) will never be sold or shared with another third party.

## What happens when you use the resolver?

When you make a DNS Query to the resolver over either `DNS-over-HTTPS` or using `DNSCrypt`, the following information is transmitted from your end:

1. Domain Name that you are querying (such as `fun.captnemo.in`)
2. Your IP Address (such as `161.23.51.1`)

The resolver then translates the domain name to an IP address by querying the authoritative nameserver for the domain (`ns.captnemo.in` for eg). This query is made by the resolver on your behalf with no information about you passed to the nameserver. It also caches this response.

### Terms of the Privacy Policy

_"Identifiable User Data"_ (below) can refer to either your IP Address, or any other information that can be used to identify you (such as a set of unique domains that you've visited).

_"Aggregate User Data"_ refers to anonymized user information, such as the number of requests received from a given IP Address over time.

This Privacy Policy guarantees the following:

1. No user data (identifiable or aggregate) will be retained beyond 1 hour.
2. Identifiable user data may be retained for upto 1 hour, in some circumstances.
3. User data in any form (identifiable or aggregate) will not be retained, sold, or transferred to any third party.
4. The resolver does not combine the data it collects with any other offering or service.
5. No entity or person will be granted any rights to the collected user data.
6. The resolver supports DNS Query Name Minimization as defined in [RFC 7816](https://rfc.me/7816).
7. The client subnet DNS extension is disabled on the resolver. This means that your IP Address or your Subnet information is not transmitted to the upstream resolver that is used.

## Explanation

The following matrix lists down all the data that the resolver receives, and what can be done to it.

Transmitted
: Refers to data being sent to the upstream nameservers.

Collected
: Data being stored locally or not.

Retention
: If the data is stored, for how long.

Usage
: What can be done with the stored data.

| Data             | Transmitted | Collected | Retention | Usage     |
| :--------------- | :---------- | --------- | --------- | --------- |
| Domain Name      | Yes         | Rarely    | 1h        | Debugging |
| Client IP/Subnet | No          | Rarely    | 1h        | Debugging |
| User Agent       | No          | No        | NA        | NA        |
| Cipher Suite     | No          | No        | NA        | NA        |
| Anything else    | No          | No        | NA        | NA        |

Debugging in the above refers to scenarios where I may turn on server logging for debugging purposes while trying to resolve an issue. This may log certain data that will be deleted as per the retention period.

### Legal Requests for Data

Legal Requests for user data will be responded to with "Data not available" since no user data is stored on the server. Legal Requests for any other information about the service will be dealt with as per the law.

## Transparency

The privacy policy for the resolver is publicly published at <https://captnemo.in/dns/privacy>. Any changes to this policy will be documented here, and communicated in advance to the Mozilla Trusted Recursive Resolver Program.

Transparency reports for the resolvers is published on an annual basis. The reports will include:

1.  Resolver Health over the last year
2.  Type and Number of user data requests received from Law Enforcement, if any.
3.  Type and Number of user data requests answered from Law Enforcement, if any.
4.  List of domains blocked throughout the year, if any.
5.  Changes in Privacy Policy, if any.
6.  Changes in Operating Principles for the resolver.

Transparency Reports for the following years are published below:

- [2017](/dns/2017/transparency.html)
- [2018](/dns/2018/transparency.html)
- [2019](/dns/2019/transparency.html) \[draft\]

# Blocking and Modification

- The resolver by default will not block or filter any domains.
- This resolver operates in Karnataka in India, and as such is subject to the jurisdiction of both the state government as well as the union government. As such, it may be specifically required by law to block or filter specific domains.
- Any domains blocked or filtered because of law enforcement requests will be listed at [/dns/blocked.txt](/dns/blocked.txt).
- The domain blocklist above will maintain a log of when particular domains are added and removed from the blocklist. It will also document which resolver the block applies to, and if possible (to the extent allowed by law), publish the corresponding Law Enforcement order.
- Accurate `NXDOMAIN` responses for absent domains will be provided.

# Operating Principles

I (Abhay Rana) run this resolver with your Privacy and Security in mind. I'm an InfoSec professional with enough experience to do this safely. The resolver runs out of the [Digital Ocean Bangalore Region][do], which is colocated with [NetMagic IT Services Private Limited][nm] in [Electronic City Bangalore][ecity]. The Data Center is both SOC1 and SOC2 certified.

The resolver is co-located on a Droplet that runs a few other personal webservices.

The objectives of the resolver:

1.  Maintaining security of the Infrastructure hosting it.
2.  Upholding privacy of the users using it.
3.  Being transparent about its operations.
4.  While running within Indian Jurisdiction.

[trr]: https://wiki.mozilla.org/Security/DOH-resolver-policy
[do]: https://www.digitalocean.com/docs/platform/availability-matrix/
[nm]: https://www.netmagicsolutions.com/data-center-in-bangalore.html
[ecity]: https://www.thehindubusinessline.com/info-tech/digitalocean-sets-up-data-centre/article8673541.ece
[v2]: https://github.com/captn3m0/captn3m0.github.com/compare/7a59c74f06f4124eb39b588e9d6f9b00b0904024...dns-privacy-draft2
