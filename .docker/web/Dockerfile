FROM php:7.4-apache

#install all the system dependencies and enable PHP modules
# unzipとかはcakePHPインストール時に使われるものをインストール
RUN apt-get update \
    && apt-get install -y \
    zip \
    nano \
    libicu-dev \
    unzip

# install required extenstions
RUN docker-php-ext-install mysqli pdo pdo_mysql intl

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#set our application folder as environment variable
ENV APACHE_DOCUMENT_ROOT=/var/www/html/webroot

ENV APACHE_LOG_DIR /var/log/apache2

ENV APACHE_RUN_DIR /var/run/apache2

ENV APACHE_LOCK_DIR /var/lock/apache2

ENV APACHE_PID_FILE /var/run/apache2/apache2.pid

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN a2enmod rewrite

COPY . /var/www/html/

CMD ["/usr/sbin/apache2", "-DFOREGROUND"]

RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "vim"]
