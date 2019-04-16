FROM xcomponent/mono:1.0.0

USER root

RUN apt-get -q update \
    && apt-get install -y \
    curl \
    apt-transport-https \
    gpg

RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | \
    gpg --dearmor | \
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null

RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ stretch main" | tee /etc/apt/sources.list.d/azure-cli.list

RUN apt-get -q update \
    && apt-get install -y \
    azure-cli \
    && rm -rf /var/lib/apt/lists/* /tmp/*

USER circleci
