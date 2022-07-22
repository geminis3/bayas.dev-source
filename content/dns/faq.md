---
title: DNS FAQ
summary: Frequently Asked Questions about my encrypted DNS service.

cover:
    image: "/img/dns.png"
---

## Why DNS over port 53 is not provided?

[Learn more about DNS amplification attacks](https://www.cloudflare.com/learning/ddos/dns-amplification-ddos-attack/).

## Are logs stored?

Yes, logs are stored for 24 hours for statistical purposes only (I promise).

## I see multiple servers on dnsleaktest.com

That's fine, several well-known upstream DNS servers are queried to provide fast response times.

## Is DNSSEC enabled?

Yes.

## Is Strict SNI enabled?

Yes.

## Is ECS enabled?

No.

## Tell me a bit about the infrastructure behind

It's basically [Adguard Home](https://github.com/AdguardTeam/AdGuardHome) running behind [Traefik](https://doc.traefik.io/traefik/) reverse proxy on a VPS server ;)

## Why do you provide this service?

I need access to my local Adguard Home instance but having a VPN connection to my house 24/7 is not an option for me so I decided to make a public instance.
