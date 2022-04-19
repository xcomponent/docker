FROM mcr.microsoft.com/dotnet/sdk:7.0

LABEL maintainer="XComponent Team <dev@xcomponent.com>"
HEALTHCHECK NONE

# Install Docker

RUN set -ex \
    && export DOCKER_VERSION=$(curl --silent --fail --retry 3 https://download.docker.com/linux/static/stable/x86_64/ | grep -o -e 'docker-[.0-9]*\.tgz' | sort -r | head -n 1) \
    && DOCKER_URL="https://download.docker.com/linux/static/stable/x86_64/${DOCKER_VERSION}" \
    && echo Docker URL: $DOCKER_URL \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/docker.tgz "${DOCKER_URL}" \
    && ls -lha /tmp/docker.tgz \
    && tar -xz -C /tmp -f /tmp/docker.tgz \
    && mv /tmp/docker/* /usr/bin \
    && rm -rf /tmp/docker /tmp/docker.tgz \
    && which docker \
    && (docker version || true) \
    && mkdir -vp ~/.docker/cli-plugins/ \
    && curl --silent -L --output ~/.docker/cli-plugins/docker-buildx https://github.com/docker/buildx/releases/download/v0.8.2/buildx-v0.8.2.linux-amd64 \
    && chmod a+x ~/.docker/cli-plugins/docker-buildx \
    && docker buildx install \
    && docker buildx version \
    && docker run --privileged --rm tonistiigi/binfmt --install all \
    && docker context create xbuilder \
    && docker buildx create xbuilder --name xbuilder --use 
