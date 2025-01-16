FROM php:8.3-fpm
ARG TIMEZONE

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    #zlibc \
    zlib1g \
    zlib1g-dev \
    libfreetype6-dev \
    libssl-dev \
    libjpeg62-turbo-dev \
    libmemcached-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libpng-dev \
    libicu-dev \
    unzip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN mkdir /.composer/ && chmod 777 /.composer/

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-configure gd
#--with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install pdo_mysql gd

# Install memcached extension
RUN apt-get update \
  && apt-get install -y libmemcached11 libmemcachedutil2 build-essential libmemcached-dev libz-dev \
  && pecl install memcached \
  && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
  && apt-get remove -y build-essential libmemcached-dev libz-dev \
  && apt-get autoremove -y \
  && apt-get clean \
  && rm -rf /tmp/pear

RUN docker-php-ext-install intl
RUN docker-php-ext-install opcache
RUN docker-php-ext-install soap

RUN apt-get install -y --no-install-recommends default-libmysqlclient-dev

RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-configure zip \
  #--with-libzip \
  && docker-php-ext-install zip

RUN docker-php-ext-install mysqli

WORKDIR /var/www/html

CMD ["php-fpm"]
