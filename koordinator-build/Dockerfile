FROM debian:stretch-slim

ENV CI true
ENV DOTNET_SDK_VERSION 2.2.401
ENV DEBIAN_FRONTEND=noninteractive
ENV MONO_VERSION 6.0.0
ENV NPM_VERSION 6.9.0

# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/etc/UTC /etc/localtime

# Use unicode
RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

RUN apt-get -q update && \
    apt-get install -y \
    curl \
    gnupg \
    apt-transport-https

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get -q update && \
    apt-get install -y --force-yes \
    build-essential \
    libsecret-1-dev \
    nodejs \
    yarn \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN npm install -g gulp-cli
RUN npm install npm@$NPM_VERSION -g

# Install Docker

# Docker.com returns the URL of the latest binary when you hit a directory listing
# We curl this URL and `grep` the version out.
# The output looks like this:

RUN set -ex \
    && export DOCKER_VERSION=$(curl --silent --fail --retry 3 https://download.docker.com/linux/static/stable/x86_64/ | grep -o -e 'docker-[.0-9]*-ce\.tgz' | sort -r | head -n 1) \
    && DOCKER_URL="https://download.docker.com/linux/static/stable/x86_64/${DOCKER_VERSION}" \
    && echo Docker URL: $DOCKER_URL \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/docker.tgz "${DOCKER_URL}" \
    && ls -lha /tmp/docker.tgz \
    && tar -xz -C /tmp -f /tmp/docker.tgz \
    && mv /tmp/docker/* /usr/bin \
    && rm -rf /tmp/docker /tmp/docker.tgz \
    && which docker \
    && (docker version || true)

# docker compose
RUN COMPOSE_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/docker-compose-latest" \
    && curl --silent --show-error --location --fail --retry 3 --output /usr/bin/docker-compose $COMPOSE_URL \
    && chmod +x /usr/bin/docker-compose \
    && docker-compose version

# install dockerize
RUN DOCKERIZE_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/dockerize-latest.tar.gz" \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/dockerize-linux-amd64.tar.gz $DOCKERIZE_URL \
    && tar -C /usr/local/bin -xzvf /tmp/dockerize-linux-amd64.tar.gz \
    && rm -rf /tmp/dockerize-linux-amd64.tar.gz \
    && dockerize --version

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" > /etc/apt/sources.list.d/mono-official-stable.list \
    && apt-get -q update \
    && apt-get install -y \
    xvfb \
    mono-devel \
    ca-certificates \
    ca-certificates-mono \
    fsharp \
    mono-vbnc \
    nuget \
    referenceassemblies-pcl \
    binutils \
    curl \
    dos2unix \
    git \
    rsync \
    sudo \
    tar \
    gzip \
    ssh \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN curl -SL --output dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-x64.tar.gz \
    && dotnet_sha512='08E1FCAFA4F898C80FF5E88EEB40C7497B4F5651AF3B8EC85F65A3DAA2F1509A766D833477358D3FF83D179E014034AB0C48120847EF24736C8D1A5B67FEC10B' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

RUN groupadd --gid 3434 circleci \
    && useradd --uid 3434 --gid circleci --shell /bin/bash --create-home circleci \
    && echo 'circleci ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-circleci \
    && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep

USER circleci
