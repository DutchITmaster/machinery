# Kerberos Open Source - Machinery

[![Build Status](https://travis-ci.org/kerberos-io/machinery.svg)](https://travis-ci.org/kerberos-io/machinery) [![Join the chat](https://img.shields.io/gitter/room/TechnologyAdvice/Stardust.svg?style=flat)](https://gitter.im/kerberos-io/hades?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Kerberos.io - video surveillance](https://kerberos.io/images/kerberos.png)](https://kerberos.io)

## License

The Kerberos Open Source project is licensed with BY-NC-SA 4.0, this means that everyone can use Kerberos and modify if to their needs, in a non commercial activity.

More information [**about this license**](https://doc.kerberos.io/opensource/license).

## Vote for features

[**Report features**](https://feathub.com/kerberos-io/machinery) if you think something is missing, and should be added to Kerberos.io, we love to hear about your ideas.

## Supported cameras

[**In this thread**](https://github.com/kerberos-io/machinery/issues/136) you can find a list of cameras that users confirmed working properly. Do you have a working camera missing from this list? Report your camera [**here**](https://github.com/kerberos-io/machinery/issues/136).

## Why Kerberos?

As burglary is very common, we believe that video surveillance is a **trivial tool** in our daily lifes which helps us to **feel** a little bit more **secure**. Responding to this need, a lot of companies have started developing their own video surveillance software in the past few years.

Nowadays we have a myriad of **expensive** cameras, recorders, and software solutions which are mainly **outdated** and **difficult** to install and use. Kerberos Open Source goal is to solve these problems and to provide every human being in this world to have their own **ecological**, **affordable**, **easy-to-use** and **innovative** surveillance solution.

## Introduction

Kerberos Open Source is perfect for personal usage. It's great if you only have a couple of surveillance cameras to be managed. A Kerberos agent (e.g. on a Raspberry Pi or inside a Docker container) runs for each camera. Their are many different installation possibilities, please have a look at [**the architecture**](https://doc.kerberos.io/architectures) or [**installation page**](https://doc.kerberos.io/opensource/installation).

Every Kerberos agent has it's own web interface (front-end) to review media recording, and processing engine (back-end) of a specific surveillance camera. The Open Source version doesn't come with a central overview of all recordings generated by your Kerberos agents. For this feature we highly recommend Kerberos cloud.

If you want to manage more than 10 Kerberos agents, it's recommended to use [**Kerberos Enterprise**](https://doc.kerberos.io/enterprise). This will help you to scale, support high availability and load balancing. Check out [**the architecture**](https://doc.kerberos.io/architectures) section for a better understanding of when to use what.

## Machinery

[**The machinery**](https://doc.kerberos.io/opensource/introduction) is the processing engine of Kerberos Open Source. It's an image processing framework, written in C++, who benefits from other third party libraries (OpenCV, etc). It takes images from the type of camera (USB-, IP- or RPi-camera) you've configured in the configuration files and executes one ore more algorithms and post-processes (e.g. save a snapshot). The configuration files allow you to define the type of camera, post-processes, conditions and much more; it's highly configurable. It's important to note that the machinery, out-of-the-box, can handle only one camera at a time.

## How does it work?

[Read more](https://doc.kerberos.io/opensource/machinery#project-structure) on our documentation website to have a better understanding of how the machinery works.

## Installation

Kerberos Open Source comes with different installation flavours (it includes both the machinery and web repository). The reason is because depending on the use case one option is better than another. A short list of recommendations:

- [**KiOS**](https://doc.kerberos.io/opensource/installation): You have a Raspberry Pi, and you only want to run a Kerberos agent on it.
- [**Raspbian**](https://doc.kerberos.io/opensource/installation): You have a Raspberry Pi, but you want other services running next to the Kerberos agent.
- [**Docker**](https://doc.kerberos.io/opensource/installation): You have a lot of IP cameras, and/or don't want to mess with dependencies.
- [**Generic**](https://doc.kerberos.io/opensource/installation): You want to develop/extend Kerberos with your own features, or you want to run a Kerberos agent on a not supported OS/architecure.

## Compile from source

Update the packages and kernel, and install some development tools.

```ts
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install git cmake subversion libav-tools dh-autoreconf libcurl4-openssl-dev yasm libx264-dev pkg-config libssl-dev
```

Install the FFmpeg library with x264 support.

```ts
git clone https://github.com/FFmpeg/FFmpeg ffmpeg
cd ffmpeg && git checkout remotes/origin/release/2.8
./configure --enable-gpl --enable-libx264 --enable-shared --prefix=/usr/local
make && sudo make install
```

Go to your home directory, or any place your prefer and pull the machinery from Github. Afterwards create a build directory and start the compilation.

```ts
cd && git clone https://github.com/kerberos-io/machinery
cd machinery && mkdir build && cd build
cmake .. && make && make check && sudo make install
```

After the machinery is build and installed succesfully, you can enable `kerberosio` to start on boot.

```ts
sudo systemctl enable kerberosio
```
