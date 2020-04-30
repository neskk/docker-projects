FROM php:7.2.30-apache-buster

LABEL author="neskk <me@neskk.com>"

# Terminal configuration
ENV TERM xterm

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    zip unzip zlib1g-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxpm-dev \
    libwebp-dev

#RUN apt autoremove -y

RUN docker-php-ext-install mysqli pdo pdo_mysql zip

RUN docker-php-ext-configure gd --with-gd \
    --with-freetype-dir --with-jpeg-dir --with-png-dir --with-xpm-dir --with-webp-dir --with-zlib-dir \
    && docker-php-ext-install gd

# Add Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Apache configuration
RUN a2enmod rewrite
RUN sed -i '$ i\ServerName localhost' /etc/apache2/apache2.conf
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf
