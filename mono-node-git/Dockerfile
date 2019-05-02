FROM xcomponent/mono-git:1.5.0
USER root
ENV CI true
ENV NPM_VERSION 6.4.1
RUN apt-get -q update && \
    apt-get install -y apt-transport-https

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

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


USER circleci
