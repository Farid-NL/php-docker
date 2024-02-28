FROM php:8.2.12-apache

ARG UID
ARG APP_USER
ARG GID
ARG APP_GROUP
ARG DEBIAN_FRONTEND=noninteractive
ARG NODE_VERSION=20
ARG POSTGRES_VERSION=15

WORKDIR /var/www/html/

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN mkdir -p /etc/apt/keyrings \
    && apt-get update \
    && apt-get install -y gnupg curl ca-certificates zip unzip git \
    && install-php-extensions pdo pdo_pgsql \
    && curl -sLS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg \
    && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_VERSION.x nodistro main" > /etc/apt/sources.list.d/nodesource.list \
    && apt-get update \
    && apt-get install -y nodejs \
    && npm install -g npm \
    && curl -sS https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | tee /etc/apt/keyrings/pgdg.gpg >/dev/null \
    && echo "deb [signed-by=/etc/apt/keyrings/pgdg.gpg] http://apt.postgresql.org/pub/repos/apt jammy-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
    && apt-get update \
    && apt-get install -y postgresql-client-$POSTGRES_VERSION \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && groupadd --force -g $GID $APP_GROUP \
    && useradd -ms /bin/bash --no-user-group -g $GID -u $UID $APP_USER \
    && a2enmod rewrite

COPY config/settings.ini /usr/local/etc/php/conf.d/settings.ini
#COPY config/settings.conf /etc/apache2/conf-enabled/settings.conf
