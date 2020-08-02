FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive
ARG MONO_VERSION=5.20
ARG MONO_URL=stable-xenial/snapshots/$MONO_VERSION

# Install Mono
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    echo "deb http://download.mono-project.com/repo/debian $MONO_URL main" > /etc/apt/sources.list.d/mono-official-stable.list && \
    apt-get update && apt-get install -y \ 
        tofrodos tzdata \
        mono-complete \
        sqlite3 mediainfo \
        && rm -rf /var/lib/apt/lists/*

# Install curl and https apt transport
RUN apt-get update && apt-get install -y curl apt-transport-https ca-certificates


# Update Node, otherwise Yarn fails
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get upgrade -y nodejs

# Install and run yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn