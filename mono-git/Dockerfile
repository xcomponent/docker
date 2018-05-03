FROM debian:stretch-slim

ENV MONO_VERSION 5.10.1.47

RUN apt-get -q update \
    && apt-get install -y gnupg

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" > /etc/apt/sources.list.d/mono-official-stable.list \
    && apt-get -q update \
	&& apt-get install -y \
    mono-devel \
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
    && rm -rf /var/lib/apt/lists/* /tmp/*