FROM php:7.1-fpm

#install xdebug
RUN pecl install xdebug \
  && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)\n" >> /usr/local/etc/php/conf.d/xdebug.ini

#install libs
RUN apt-get update \
    && apt-get install -y \
    zip \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libpng12-dev
RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install \
    exif \
    gd \
    intl \
    pdo_mysql

#setup user access
RUN usermod -u 1000 www-data

RUN chown -R /var/www

#install composer
RUN curl https://getcomposer.org/installer  \
    | php -- --filename=composer --install-dir=/bin

RUN composer config --global repo.packagist composer https://packagist.org

#install gulp
RUN apt-get install -y \
    npm \
    && npm install n -g \
    && n stable \
    && npm install yarn -g


RUN apt-get install -y nano
