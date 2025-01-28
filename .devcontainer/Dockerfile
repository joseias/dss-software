FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update  -y \
    && apt-get install -y --no-install-recommends ca-certificates apt-transport-https software-properties-common
    
# locale issues with pa:ondrej/php
#RUN apt-get update  -y \
#    && apt-get install -y --no-install-recommends language-pack-en-base
  
#RUN export LC_ALL=en_US.UTF-8 \
#    && export LANG=en_US.UTF-8 \
#    && apt-get install -y --no-install-recommends gpg-agent 
#    && LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php

RUN apt-get update -y \
    && apt-get install -y --no-install-recommends php8.3 php8.3-bcmath php8.3-mbstring \
    && apt-get install -y --no-install-recommends php8.3-xml php8.3-mysql php8.3-curl \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --set php /usr/bin/php8.3


# install composer globally
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends curl \
    && curl https://getcomposer.org/download/2.8.4/composer.phar --output /tmp/composer \
    && mv /tmp/composer /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer


#MySQL
# in docker-compose


#Adminer
# in docker-compose


# Git
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends git



# Other utilities
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends unzip p7zip-full 



# from VS Code 
#FROM mcr.microsoft.com/devcontainers/php:1-8.1-bullseye
# Install MariaDB client
# Install php-mysql driver
#RUN docker-php-ext-install mysqli pdo pdo_mysql

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

