FROM xcomponent/mono-node-git:1.7.0
USER root
ENV CI true
RUN apt-get -q update && \
    apt-get install -y \
    xvfb \
    x11-xkb-utils \
    xfonts-100dpi \
    xfonts-75dpi \
    xfonts-scalable \
    xfonts-cyrillic \
    x11-apps \
    clang \
    libdbus-1-dev \
    libgtk2.0-dev \
    libnotify-dev \
    libgnome-keyring-dev \
    libgconf2-dev \
    libasound2-dev \
    libcap-dev \
    libcups2-dev \
    libxtst-dev \
    libxss1 \
    libnss3-dev \
    gcc-multilib \
    g++-multilib \
    rabbitmq-server \
    && rm -rf /var/lib/apt/lists/* /tmp/*
USER circleci
