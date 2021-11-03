---
title: "Turn off your dedicated Nvidia GPU with udev rules"
summary: Save battery on your Optimus / gaming laptop by disabling the Nvidia GPU when you don't use it.
date: 2021-10-14
---

### GUI app to toggle ON/OFF your Nvidia GPU in just one-click is coming soon... 👀

Nvidia GPUs on Linux have always been a headache due to their propietary drivers, but this problem gets worse on Optimus laptops due to **inexistent dynamic power management** technologies on **pre-Turing cards** paired with Intel processors older than Coffee Lake. [See official Nvidia documentation on dynamic PM for Turing and newer cards](http://us.download.nvidia.com/XFree86/Linux-x86_64/465.31/README/dynamicpowermanagement.html).

Turning off your Nvidia GPU will result in lower battery consumption when you don't need it (eg coding, watching videos, etc).

## 1. Blacklist nouveau and nvidia modules

Create the file `/etc/modprobe.d/block-nvidia.conf`:

    blacklist i2c_nvidia_gpu
    blacklist nouveau
    blacklist nvidia
    blacklist nvidia-drm
    blacklist nvidia-modeset

## 2. Udev rules

Create the file `/lib/udev/rules.d/50-disable-nvidia.rules`:

    # Remove NVIDIA USB xHCI Host Controller devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x0c0330", ATTR{remove}="1"

    # Remove NVIDIA USB Type-C UCSI devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x0c8000", ATTR{remove}="1"

    # Remove NVIDIA Audio devices, if present
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x040300", ATTR{remove}="1"

    # Remove NVIDIA VGA/3D controller
    ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x10de", ATTR{class}=="0x03[0-9]*", ATTR{remove}="1"


Then reboot.

## 3. Reverting

Just delete the created files and reboot.

## 4. Final thoughts

{{< youtube _36yNWw_07g >}}
