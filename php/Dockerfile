FROM php:fpm

WORKDIR  /var/www

RUN apt-get update

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot && rm -f /tmp/composer-setup.*

RUN docker-php-ext-install pdo_mysql mysqli

#php-gd
RUN apt-get install -y libfreetype6-dev libmcrypt-dev libjpeg-dev libpng-dev
RUN docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include \
        --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd

#php-zip
RUN apt-get install -y libzip-dev  zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip

#php-imagick
RUN apt-get install -y libmagickwand-dev --no-install-recommends && \
    pecl install imagick && docker-php-ext-enable imagick

RUN pecl install redis  && docker-php-ext-enable redis

#RUN pecl install xdebug && docker-php-ext-enable xdebug


RUN apt-get install -y libmemcached-dev zlib1g-dev	\
	&& pecl install memcached && docker-php-ext-enable memcached


