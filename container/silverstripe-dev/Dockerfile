ARG PHP_VERSION
FROM php:${PHP_VERSION}-apache AS devenv
ENV DEBIAN_FRONTEND=noninteractive

# ----------------------
#   Silverstripe
# ----------------------
# Configure apache & PHP
ENV DOCUMENT_ROOT=/var/www/html
ENV APACHE_SERVER_NAME=localhost
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/install-php-extensions
RUN set -eux; \
    install-php-extensions \
        bcmath \
        mysqli \
        pdo \
        pdo_mysql \
        intl \
        ldap \
        gd \
        soap \
        tidy \
        xsl \
        zip \
        exif \
        gmp \
        opcache; \
    \
    docker-php-ext-configure opcache --enable-opcache; \
    docker-php-ext-install opcache; \
    a2enmod rewrite expires remoteip headers; \
    \
    echo 'date.timezone = Europe/Zurich' > "$PHP_INI_DIR/conf.d/timezone.ini"; \
    { \
        echo 'log_errors = On'; \
        echo 'error_log = /dev/stderr'; \
    } > "$PHP_INI_DIR/conf.d/errors.ini"
COPY srv_conf/opcache.ini $PHP_INI_DIR/conf.d/
COPY srv_conf/memory.ini $PHP_INI_DIR/conf.d/
COPY srv_conf/000-default.conf $APACHE_CONFDIR/sites-available/

# ----------------------
#   Composer
# ----------------------
RUN set -eux; \
    apt-get update -qq; \
    apt-get install git vim unzip -yqq; \
    rm -rf /var/lib/apt/lists/*
COPY --from=composer /usr/bin/composer /usr/bin/composer

# ----------------------
#   Chromedriver
# ----------------------
# FROM devenv AS devenv-cdr
# RUN set -eux; \
#     apt update -qq; \
#     apt install wget unzip libnss3 gnupg -yqq; \
#     wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor | tee /usr/share/keyrings/google-chrome.gpg >> /dev/null;\
#     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome.gpg] http://dl.google.com/linux/chrome/deb/ stable main" | tee /etc/apt/sources.list.d/google-chrome.list ;\
#     # echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list ;\
#     apt update -qq; \
#     apt install google-chrome-stable -yqq; \
#     rm -rf /var/lib/apt/lists/*
# # Install chromedriver
# RUN VERSION=$(curl http://chromedriver.storage.googleapis.com/LATEST_RELEASE); \
#     wget https://chromedriver.storage.googleapis.com/$VERSION/chromedriver_linux64.zip; \
#     unzip chromedriver_linux64.zip; \
#     mv chromedriver /usr/bin/chromedriver
# EXPOSE 9515
