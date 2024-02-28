FROM php:8.2.12-apache

# Arguments for creating a non-root user
ARG UID
ARG APP_USER
ARG GID
ARG APP_GROUP

# Frontend for automatic installs
ARG DEBIAN_FRONTEND=noninteractive

# Versions of other software
ARG NODE_VERSION=20
ARG POSTGRES_VERSION=15

# Argument to change the default document root of Apache
ARG A_DOCUMENT_ROOT
# Default: /var/www/html
ENV DOCUMENT_ROOT=$A_DOCUMENT_ROOT

WORKDIR /var/www/html

# Script to facilitate the installation of php extensions
ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

COPY config/settings.ini /usr/local/etc/php/conf.d/settings.ini
#COPY config/settings.conf /etc/apache2/conf-available/settings.conf
#COPY config/vh.conf /etc/apache2/sites-available/vh.conf

RUN mkdir -p /etc/apt/keyrings \
    && apt-get update \
    && apt-get install -y gnupg curl ca-certificates zip unzip git \
    && install-php-extensions pdo pdo_pgsql pgsql \
    && curl -sLS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg \
    && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_VERSION.x nodistro main" > /etc/apt/sources.list.d/nodesource.list \
    && apt-get update \
    && apt-get install -y nodejs \
    && npm install -g npm \
    && curl -sS https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | tee /etc/apt/keyrings/pgdg.gpg >/dev/null \
    && echo "deb [signed-by=/etc/apt/keyrings/pgdg.gpg] http://apt.postgresql.org/pub/repos/apt jammy-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
    && apt-get update \
    && apt-get install -y postgresql-client-"$POSTGRES_VERSION" \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && groupadd --force -g "$GID" "$APP_GROUP" \
    && useradd -ms /bin/bash --no-user-group -g "$GID" -u "$UID" "$APP_USER" \
    && a2enmod rewrite \
#    && a2enconf settings.conf \
#    && a2ensite vh.conf \
    && if [ -n "$DOCUMENT_ROOT" ] && [ "$DOCUMENT_ROOT" != "/var/www/html" ]; then \
           sed -ri -e "s!/var/www/html!${DOCUMENT_ROOT}!g" /etc/apache2/sites-available/*.conf; \
           sed -ri -e "s!/var/www/!${DOCUMENT_ROOT}!g" /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf; \
       fi

#USER dev
