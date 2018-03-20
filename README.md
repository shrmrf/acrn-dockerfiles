# Build containers for Project ACRN

## Introduction

This repository contains a number of Dockerfile that include
all the build tools and dependencies to build the ACRN Project
components, i.e. the `acrn-hypervisor` and `acrn-devicemodel`

The workflow is pretty simple and can be summarized in these few steps:

1. Build the *build containers* based on your preferred OS
1. Clone the Project ACRN repositories
1. Start the build container and give it the repositories
1. Build the Project ACRN components

The pre-requisite is that you have Docker installed on your machine.
Explaining how to install it on your system is beyond the scope of this
document, please visit https://www.docker.com for detailed instructions.

## Build the *build containers*

Each `Dockerfile` in this repo has an extension that tells what Linux
distribution it is based on. To build a container using any of those,
use this command:
```
$ sudo docker build -t <container-name> -f Dockerfile.<baseos> .
```

As an example, to build a container based on CentOS 7, do:
```
$ sudo docker build -t centos7 -f Dockerfile.centos7 .
```

## Clone Project ACRN

Follow these simple steps to clone the Project ACRN repositories
```
$ mkdir ~/acrn
$ cd ~/acrn
$ git clone https://github.com/projectacrn/acrn-hypervisor
$ git clone https://github.com/projectacrn/acrn-devicemodel
```

## Start the build container

Use this `~/acrn` folder and pass it on to your build container:
```
$ cd ~/acrn
$ sudo docker run -ti -v $PWD:/root/acrn <container-name>
```

Using CentOS 7 again as an example, that gives us:
```
$ cd ~/acrn
$ sudo docker run -ti -v $PWD:/root/acrn centos7
```

## Build the ACRN components

The steps above place you inside the container and give you access to
the Project ACRN repositories you cloned earlier. You can now build any
of the components. Here is an example:
```
# cd acrn-hypervisor
# make PLATFORM=uefi RELEASE=1
```
