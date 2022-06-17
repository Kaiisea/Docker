FROM php:8.0-fpm

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    build-essential \
    zip \
    unzip \
    git \
    curl

#RUN pecl install xdebug-3.0.0 && docker-php-ext-enable xdebug

RUN apt-get update && \
apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev && \
docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ && \
docker-php-ext-install gd

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www
RUN echo "root:secret" | chpasswd

USER www

EXPOSE 9000

CMD ["php-fpm"]