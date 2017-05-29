# jenkins-slave-mono

This image is used to create a jenkins slave dedicated to mono/cake compilations.
> It is important to notice that git is already installed in this image.

## How to use this image

### Run

```
$ docker run -it -d -p ${JENKINS_SSH_PORT}:22 --rm --name docker_mono xcomponent/jenkins-slave-mono:1.0.1
```
* ${JENKINS_SSH_PORT}: port used by jenkins to connect to this node 

### Stop

```
$ docker stop docker_mono
```

### Jenkins node configuration

* Remote root directory: /jenkins
* Launch method: Launch slave agents with SSH
* SSH port: ${JENKINS_SSH_PORT}
* SSH credentials: jenkins/jenkins

## Build this image

```
$ docker build -t xcomponent/jenkins-slave-mono:1.0.1 .
```

## GitHub project

[https://github.com/xcomponent/docker](https://github.com/xcomponent/docker)
