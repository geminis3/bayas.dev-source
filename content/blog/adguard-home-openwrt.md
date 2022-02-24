---
title: "How to install Adguard Home on your OpenWrt router"
summary: Block ads, spyware and speed up browsing with powerful DNS filtering at the router level.
date: 2021-10-14

cover:
    image: "https://ph-files.imgix.net/7abb8658-2235-4f9f-a1fc-5d3cd3f20779.png?auto=format%2Ccompress%2Cenhance&dpr=1&crop=false&fit=max&w&h=1"
---

AdGuard Home is a network-wide software for blocking ads & tracking. After you set it up, it'll cover ALL your home devices, and you don't need any client-side software for that.

It operates as a DNS server that re-routes tracking domains to a "black hole", thus preventing your devices from connecting to those servers.

Compared to Pi-Hole, Adguard Home doesn't requires additional dependencies so you can run it on OpenWrt without problems.

## System requirements

- A router with a recent OpenWrt version installed.
- 100MB free RAM.
- 20MB free disk space.

For this tutorial I'm going to use a [Belkin RT3200 / Linksys E8450](https://openwrt.org/toh/linksys/e8450).

## 1. Installation

This router has an arm64 processor but you may need to replace it with the architecture that matches your router (eg armv7, mips, etc), SSH into your router and run:

    opkg update && opkg install wget
    mkdir /opt/ && cd /opt/
    wget -c https://static.adguard.com/adguardhome/release/AdGuardHome_linux_arm64.tar.gz
    tar xfvz AdGuardHome_linux_arm64.tar.gz
    rm AdGuardHome_linux_arm64.tar.gz
    /opt/AdGuardHome/AdGuardHome -s install

## 2. Setup AGH

Note that if your router is not at 192.168.1.1 then replace the IP address accordingly.

- Go to 192.168.1.1:3000.
- Setup the admin web interface to listen in 192.168.1.1 at port 8080.
- Set DNS server to listen in 192.168.1.1 at port 5353.
- Create an user and choose a strong password.

## 3. Point your DNS to the AGH instance

- Login into LuCi and go to DHCP and DNS section, set DNS forwardings to 192.168.1.1#5353.
- Go to Resolv and Hosts Files tab and check the Ignore resolv file option.

## 3.1 Redirect all DNS traffic to AGH

**This step is optional**, there are some apps and devices that ship with a harcoded DNS server making AGH useless unless we setup the following iptables rules:

    iptables -t nat -A PREROUTING -i br-lan -p udp --dport 53 -j DNAT --to 192.168.1.1:5353
    iptables -t nat -A PREROUTING -i br-lan -p tcp --dport 53 -j DNAT --to 192.168.1.1:5353

## 3. Enjoy

Feel free to change upstream DNS servers to whatever you like (Adguard Home supports DoH, DoT and DoQ out of the box), add the blacklists of your preference and enjoy ad-free browsing on all of your devices. 

![adguard dashboard](/img/agh-dashboard.png)
