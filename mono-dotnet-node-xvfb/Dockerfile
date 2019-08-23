FROM xcomponent/mono-node-git-xvfb:1.7.0
USER root
ENV CI true
ENV DOTNET_SDK_VERSION 2.2.401
RUN apt-get -q update && \
    apt-get install -y \
    ant \
    libc6 \
    libgcc1 \
    libgssapi-krb5-2 \
    libicu57 \
    liblttng-ust0 \
    libssl1.0.2 \
    libstdc++6 \
    openjdk-8-jdk \
    zlib1g \
    ca-certificates-java && \
    update-ca-certificates -f && \
    rm -rf /var/lib/apt/lists/* /tmp/*

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN curl -SL --output dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-x64.tar.gz \
    && dotnet_sha512='08E1FCAFA4F898C80FF5E88EEB40C7497B4F5651AF3B8EC85F65A3DAA2F1509A766D833477358D3FF83D179E014034AB0C48120847EF24736C8D1A5B67FEC10B' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

USER circleci
