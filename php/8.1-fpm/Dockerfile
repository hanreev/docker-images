FROM php:8.1-fpm

ARG pgsql

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y \
  libzip-dev \
  libpng-dev \
  libjpeg62-turbo-dev \
  libwebp-dev \
  libfreetype6-dev \
  && apt-mark manual \
  libzip4 \
  libpng16-16 \
  libjpeg62-turbo \
  libwebp6 \
  libfreetype6

RUN docker-php-ext-install pdo_mysql zip

RUN docker-php-ext-configure gd \
  --with-jpeg=/usr/include \
  --with-webp=/usr/include \
  --with-freetype=/usr/include \
  && docker-php-ext-install gd

RUN if [ ! -z "${pgsql}" ]; then \
  apt-get install -y libpq-dev && apt-mark manual libpq5; \
  docker-php-ext-install pgsql pdo_pgsql; \
  apt-get purge -y libpq-dev; \
  fi

# Purge unused packages and clear cache
RUN apt-get purge -y \
  libzip-dev \
  libpng-dev \
  libjpeg62-turbo-dev \
  libwebp-dev \
  libfreetype6-dev \
  && apt-get autoremove -y --purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www

USER www-data

CMD [ "bash" ]
