FROM php:8.4-fpm

# カレントディレクトリの設定
# なおdocker-compose.yml側でapp側のvar/srcにマウントさせていることには注意すること
WORKDIR /var/www/src

# Copy PHP config
COPY php.ini /usr/local/etc/php/

# PHP-FPMのために9000番を開ける
EXPOSE 9000

# Install system dependencies, LibreOffice, and clean up
RUN apt-get update && apt-get install -y locales \
        curl \
        wget \
        make \
        zlib1g-dev \
        libzip-dev \
        zip \
        unzip \
        default-mysql-client \
        fonts-ipaexfont \
    && echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=ja_JP.UTF-8 \
    && export LANG=ja_JP.UTF-8 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \

# Optional: コンテナ内でUTF-8を設定
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

# Install PHP extensions
RUN docker-php-ext-install zip pdo_mysql

# Install Composer and Laravel installer
RUN curl -s https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer global require "laravel/installer"

# Install Node.js (latest) and PM2
RUN curl -fsSL https://deb.nodesource.com/setup_current.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g npm@latest dotenv

# Confirm versions
RUN node --version && npm --version

# php-fpm実行
CMD ["php-fpm"]