FROM xcomponent/mono-git:1.0.2

ENV CI true
RUN apt-get -q update && \
	apt-get install -y apt-transport-https

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

RUN apt-get -q update && \
    apt-get install -y --force-yes \
    build-essential \
    libsecret-1-dev \
    nodejs \
    yarn

RUN npm install -g gulp-cli