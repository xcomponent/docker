# mono-node-git-xvfb

[![Docker Pulls](https://img.shields.io/docker/pulls/xcomponent/mono-node-git-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-node-git-xvfb)
[![](https://images.microbadger.com/badges/version/xcomponent/mono-node-git-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-node-git-xvfb)
[![](https://images.microbadger.com/badges/image/xcomponent/mono-node-git-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-node-git-xvfb)

This image is used to get a mono / node 8 environment with xvfb (to run integration tests with codeceptjs for example).
It can be used to build mono/node projects in a continuous integration environment such as CircleCI.

## How to use this image

### Run

```
$ docker run -it xcomponent/mono-node-git-xvfb:1.3.2
```

## Build this image

```
$ docker build -t xcomponent/mono-node-git-xvfb:1.3.2 .
```

## GitHub project

[https://github.com/xcomponent/docker](https://github.com/xcomponent/docker)
