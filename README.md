# [wslph/mmc](https://hub.docker.com/r/wslph/mmc)

- [Introduction](#introduction)
    - [Changelog](Changelog.md)
- [Contributing](#contributing)
- [Issues](#issues)
- [Announcements](https://git.whiteskylabs.com/mulesoft/docker-mmc/issues)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [References](#references)
- [About](#about)

---
# Introduction

Docker [Mule Management Console](https://docs.mulesoft.com/mule-management-console/v/3.8/) container.

---
# Contributing

If you find this image useful here's how you can help:

- Be a part of the community and help resolve [Issues](https://git.whiteskylabs.com/mulesoft/docker-mmc/issues)

---
# Issues

Docker is a relatively new project and is active being developed and tested by a thriving community of developers and testers, and every release includes many enhancements and bugfixes.

Given the nature of the development and release cycle it is very important that you have the latest version of Docker installed because any issue that you encounter might have already been fixed with a newer Docker release.

Install the most recent version of the Docker Engine for your platform using the [official Docker releases](http://docs.docker.com/engine/installation/), which can also be installed using:

```bash
wget -qO- https://get.docker.com/ | sh
```

Fedora and RHEL/CentOS users should try disabling selinux with `setenforce 0` and check if resolves the issue. If it does than there is not much that I can help you with. You can either stick with selinux disabled (not recommended by redhat) or switch to using ubuntu.

If using the latest docker version and/or disabling selinux does not fix the issue then please file a issue request on the [issues](https://git.whiteskylabs.com/mulesoft/docker-mmc/issues) page.

In your issue report please make sure you provide the following information:

- The host distribution and release version.
- Output of the `docker version` command
- Output of the `docker info` command
- The `docker run` command you used to run the image (mask out the sensitive bits).

---
# Prerequisites

Your docker host needs to have at least 4GB (or more) of available RAM to run Mule Management Console. Please refer to the [hardware requirements](https://docs.mulesoft.com/mule-user-guide/v/3.7/hardware-and-software-requirements) documentation for additional information.

---
# Installation

Automated builds of the image are available on [Dockerhub](https://hub.docker.com/r/wslph/mmc) and is the recommended method of installation.


```bash
docker pull wslph/mmc:latest
```

Example 1 : Launching  Mule Management Console

```bash
docker run --restart=always --name mmc -d \
    --publish 8080:8080 \
    wslph/mmc:latest
```

Example 1 : Launching  Mule Management Console with persistent `mmc-data` and tomcat `logs`

```bash
docker run --restart=always --name mmc -d \
    --publish 8080:8080 \
    --volume ~/mmc/logs:/opt/tomcat/logs \
    --volume ~/mmc/data:/opt/tomcat/mmc-data \
    wslph/mmc:latest && docker logs -f mmc
```

You can then access it via `http://<host>:8080/`, with the following default username as `admin` and password as `admin`


__NOTE__: Please allow a couple of minutes for the Mule Management Console to start. Check the logs by running `docker logs -f mmc` to verify its status.


---
# Maintenance

**Shell Access**

For debugging and maintenance purposes you may want access the container's shell. If you are using docker version `1.3.0` or higher you can access a running container's shell using `docker exec` command.

```bash
docker exec -it mmc bash
```
---
# References

* Container is based from [wslph/ubuntu:xenial-latest](https://hub.docker.com/r/wslph/ubuntu)
* Container is installed with the latest [Oracle JDK8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* As of this build, container is built with [Apache Tomcat 9.0.0.M19](http://tomcat.apache.org/tomcat-9.0-doc/)
* As of this build, the latest version of `mmc-console` packaged in this container is `3.8.2`

---
# About
Developed and maintained by [WhiteSky Labs](https://www.whiteskylabs.com), a Premier Partner of [MuleSoft®](https://www.mulesoft.com/) with the mission to be the #1 Certified Partner to deliver specialized API integration services.
