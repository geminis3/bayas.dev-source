---
title: "Building Docker images for multiple architectures"
summary: "Learn how to use the Docker buildx tool to build images for ARM/ARM64 devices from a x86_64 Linux machine."
date: 2022-02-24

cover:
    image: "https://terminalwiki.com/wp-content/uploads/2021/04/install-docker-on-a-raspberry-pi.jpg"
---

In this post we'll learn how to create multi-architecture Docker images, this is useful for developing/deploying applications on non x86_64 devices such as a Raspberry Pi (ARM64).


If you aren't familiar with Docker or don't know what is it, [checkout its Getting Started guide](https://docs.docker.com/get-started/) first. 

## System requirements
- Linux
- Docker

For this guide I'm going to use Ubuntu 21.10 as my host (package names may vary on other distros).

## 1. Install Docker buildx (optional)
Ubuntu packaged version of Docker doesn't include buildx, so we need to install it manually:

1. (Grab the latest release)[https://github.com/docker/buildx/releases/latest]
2. Copy it to `~/.docker/cli-plugins`
3. Make it executable
```
chmod +x ~/.docker/cli-plugins/docker-buildx
```

## 2. Install the required dependencies
Docker buildx works by using QEMU to emulate foreign CPU architectures on our host machine, we need to install the following packages:
```
sudo apt-get install qemu-user-static binfmt-support
```

## 3. Using buildx

### 3.1 Create a builder
Before using buildx we need to create a new builder instance, you can name it to whatever you want but I'm going to name it `mybuilder` for this guide:
```
docker buildx create --name mybuilder
docker buildx use mybuilder
```
We can check the status and supported CPU architectures of our builder with:
```
docker buildx inspect --bootstrap
```

### 3.2 Building an image
Now we're ready to build multi-architecture Docker images with the following command:
```
docker buildx build \
--push \
--platform linux/arm64/v8,linux/amd64 \
--tag <username>/<image-name>:<tag> .
```

> This process may take a while depending on several factors

#### 3.2.1 Command breakdown
- `--push` will upload our freshly built images to the Docker Hub
- `--platform` specifies the CPU architectures that we'll build for, in this case ARM64 v8 and AMD64 (x86_64)

Have fun!