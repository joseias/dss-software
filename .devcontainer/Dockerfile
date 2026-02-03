FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive
ARG USERNAME=dss

# basic dependencies
RUN apt-get update  -y \
    && apt-get install -y --no-install-recommends ca-certificates apt-transport-https software-properties-common curl
    

RUN apt-get update -y \
    && apt-get install -y --no-install-recommends php8.3 php8.3-bcmath php8.3-mbstring \
    && apt-get install -y --no-install-recommends php8.3-xml php8.3-mysql php8.3-curl \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*


RUN update-alternatives --set php /usr/bin/php8.3


# composer
RUN curl https://getcomposer.org/download/2.9.3/composer.phar --output /tmp/composer \
    && mv /tmp/composer /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer




# mysql
# in docker-compose


# adminer
# in docker-compose


# git
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends git


# other utilities
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends unzip p7zip-full 

# create the user early so tools installed below are owned by them
RUN groupadd $USERNAME \
    && useradd -g $USERNAME -m -s /bin/bash $USERNAME \
    # [optional] add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update -y \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install Node.js via NodeSource for a reproducible Docker build
ARG NODE_VERSION=24
RUN curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Configure npm for the `dss` user to allow global installs without sudo
RUN mkdir -p /home/${USERNAME}/.npm-global \
    && chown -R ${USERNAME}:${USERNAME} /home/${USERNAME} \
    && su - ${USERNAME} -s /bin/bash -c "npm config set prefix /home/${USERNAME}/.npm-global" \
    && echo 'export PATH=$HOME/.npm-global/bin:$PATH' >> /home/${USERNAME}/.profile \
    && chown ${USERNAME}:${USERNAME} /home/${USERNAME}/.profile

# [optional] set the default user. Omit if you want to keep the default as root.
USER $USERNAME
