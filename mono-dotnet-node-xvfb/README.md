# mono-dotnet-node-xvfb

[![Docker Pulls](https://img.shields.io/docker/pulls/xcomponent/mono-dotnet-node-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-dotnet-node-xvfb)
[![](https://images.microbadger.com/badges/version/xcomponent/mono-dotnet-node-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-dotnet-node-xvfb)
[![](https://images.microbadger.com/badges/image/xcomponent/mono-dotnet-node-xvfb.svg)](https://store.docker.com/community/images/xcomponent/mono-dotnet-node-xvfb)

This image is used to get a mono / dotnet / node 8 environment with xvfb (to run integration tests with codeceptjs for example).
It can be used to build mono/node projects in a continuous integration environment such as CircleCI.

## How to use this image

### Run

```
$ docker run -it xcomponent/mono-dotnet-node-xvfb:1.8.0
```

## Build this image

```
$ docker build -t xcomponent/mono-dotnet-node-xvfb:1.8.0 .
```

## GitHub project

[https://github.com/xcomponent/docker](https://github.com/xcomponent/docker)
