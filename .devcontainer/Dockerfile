FROM gcc:14

LABEL maintainer="haessal@mizutamauki.net"

ENV DEBIAN_FRONTEND=noninteractive

# upgrade packages and install common tools
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
            ca-certificates \
            curl \
            git \
            less \
            locales \
            openssh-client \
            tzdata \
            vim \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install tools to build and debug
RUN apt-get update && apt-get install -y --no-install-recommends \
            cmake \
            gdb \
            lcov \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install python and tools
RUN apt-get update && apt-get install -y --no-install-recommends \
            python3 \
            python3-pip \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install GoogleTest (download source and build)
RUN apt-get update && apt-get install -y --no-install-recommends \
            googletest \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
        && mkdir googletest-build-work && cd googletest-build-work \
        && cmake /usr/src/googletest/ && make && make install \
        && cd .. && rm -R googletest-build-work

# add user for vscode
RUN useradd -m vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
COPY .bash_aliases /home/vscode/.bash_aliases
WORKDIR /workspaces
