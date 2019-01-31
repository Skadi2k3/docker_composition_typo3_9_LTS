FROM php:7.2.1-apache
ENV APACHE_DOCUMENT_ROOT /var/www/typo3/public
LABEL maintainer="egidio docile"
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN apt-get update && apt-get install -y -qq wget
RUN cd ~ && wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet && mv composer.phar /usr/local/bin/composer
RUN apt-get install -y -qq zlib1g-dev freetype* ghostscript imagemagick
RUN apt-get install -y -qq libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN pecl -q install imagick >/dev/null 2>&1 || { retVal=$?; true; }
RUN docker-php-ext-enable imagick
RUN apt-get update && apt-get install -y libwebp-dev libjpeg62-turbo-dev libpng-dev libxpm-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir --enable-gd-native-ttf
RUN docker-php-ext-install pdo pdo_mysql mysqli zip gd
RUN a2enmod deflate filter mime expires setenvif headers rewrite authz_core alias autoindex 