FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive
ARG USERNAME=dss

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


# Create the user
RUN groupadd $USERNAME \
    && useradd -g $USERNAME -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update -y \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME