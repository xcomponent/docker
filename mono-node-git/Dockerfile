FROM xcomponent/mono-git:1.2.0

ENV CI true
ENV NPM_VERSION 6.0.1
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