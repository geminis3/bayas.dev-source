---
title: DNS setup guide
summary: Learn how to use my encrypted DNS service on all your devices.

cover:
    image: "/img/dns.png"
---

Learn how to use my encrypted DNS server on all your devices.

## Android 9.0 and later

1. Open your device’s Settings.
2. Navigate to Network & internet -> Advanced -> Private DNS.
3. Select Private DNS provider hostname.
4. In the textbox, type `dns.bayas.dev` or `dns-family.bayas.dev`
5. Click Save.

## iOS 14 and later

### Regular Server

- [DNS over HTTPS (DoH) profile](/resources/doh.mobileconfig)
- [DNS over TLS (DoT) profile](/resources/dot.mobileconfig)

### Family Safe Server

- [DNS over HTTPS (DoH) profile](/resources/doh-family.mobileconfig)
- [DNS over TLS (DoT) profile](/resources/dot-family.mobileconfig)

1. Press “Allow” if asked to allow download.
2. In iOS, go to Settings -> General -> Device Management.
3. Press on the newly downloaded profile.
4. Press “Install” in upper right corner.
5. Fill in your password and press “install” until complete.

## OpenWrt router

- [https-dns-proxy tutorial by Van Tech Corner](https://www.youtube.com/watch?v=ySkqc_7Xc3U)

## Web Browsers (Chrome, Edge, Brave, Firefox)

- [DNS over HTTPS guide by gHacks](https://www.ghacks.net/2021/10/23/how-to-enable-dns-over-https-secure-dns-in-chrome-brave-edge-firefox-and-other-browsers/)
