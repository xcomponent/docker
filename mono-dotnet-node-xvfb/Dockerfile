FROM xcomponent/mono-node-git-xvfb:1.4.0
USER root
ENV CI true
ENV DOTNET_SDK_VERSION 2.2.203
RUN apt-get -q update && \
    apt-get install -y \
    libc6 \
    libgcc1 \
    libgssapi-krb5-2 \
    libicu57 \
    liblttng-ust0 \
    libssl1.0.2 \
    libstdc++6 \
    zlib1g \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN curl -SL --output dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-x64.tar.gz \
    && dotnet_sha512='8da955fa0aeebb6513a6e8c4c23472286ed78bd5533af37d79a4f2c42060e736fda5fd48b61bf5aec10bba96eb2610facc0f8a458823d374e1d437b26ba61a5c' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

USER circleci