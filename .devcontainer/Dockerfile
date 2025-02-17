FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive
ARG USERNAME=dss

RUN apt-get update  -y \
    && apt-get install -y --no-install-recommends ca-certificates apt-transport-https software-properties-common
    

RUN apt-get update -y \
    && apt-get install -y --no-install-recommends php8.3 php8.3-bcmath php8.3-mbstring \
    && apt-get install -y --no-install-recommends php8.3-xml php8.3-mysql php8.3-curl \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*


    RUN update-alternatives --set php /usr/bin/php8.3


# composer
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends curl \
    && curl https://getcomposer.org/download/2.8.4/composer.phar --output /tmp/composer \
    && mv /tmp/composer /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer


# node and npm
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends nodejs npm


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


# create the user
RUN groupadd $USERNAME \
    && useradd -g $USERNAME -m $USERNAME \
    # [optional] add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update -y \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME


# [optional] set the default user. Omit if you want to keep the default as root.
USER $USERNAME