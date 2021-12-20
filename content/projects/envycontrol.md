---
title: "EnvyControl"
summary: Easy GPU switching for Nvidia Optimus laptops under Linux.
aliases: ["/simplyarch"]
tags: ["projects", "linux"]
---

<iframe src="https://ghbtns.com/github-btn.html?user=geminis3&repo=envycontrol&type=star&count=true&size=large" frameborder="0" scrolling="0" width="170" height="30" title="GitHub"></iframe><br>

EnvyControl is a program aimed to provide an easy way to switch GPU modes on Nvidia Optimus systems (i.e laptops with Intel + Nvidia or AMD + Nvidia configurations) under Linux.

## Get EnvyControl ⬇️

Install the [envycontrol](https://aur.archlinux.org/packages/envycontrol/) package with the AUR helper of your choice, if not on Arch Linux you can run `envycontrol.py` from source.

## Usage 📖

```
usage: envycontrol [-h] [--status] [--switch MODE] [--version]

options:
  -h, --help     show this help message and exit
  --status       Query the current graphics mode set by EnvyControl
  --switch MODE  Switch the graphics mode. You need to reboot for changes to
                 apply. Supported modes: integrated, nvidia, hybrid
  --version, -v  Print the current version and exit
```

### Examples 🚀

Set graphics mode to `integrated` (disable the Nvidia GPU):

```
sudo envycontrol --switch integrated
```

Show the current graphics mode:

```
envycontrol --status
```

## Gift me a star ⭐️

https://github.com/geminis3/EnvyControl