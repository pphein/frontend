ARG PHP_VERSION=8.2

FROM php:${PHP_VERSION}-cli

ARG USER=dev
ARG UID=1000
ARG GID=1000

# Install composer
RUN curl -sSL https://getcomposer.org/installer | php \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer

# Add non-root user
RUN groupadd --gid $GID $USER \
    && useradd --uid $UID --gid $GID -m $USER

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install git zip zsh curl vim

# Install and enable xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN mysqli

RUN echo 'xdebug.mode=coverage' >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

USER ${USER}

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# User
RUN composer global require squizlabs/php_codesniffer
