FROM php:7.1-fpm

RUN apt-get update && apt-get install -y \
  bzip2 \
  libcurl4-openssl-dev \
  libicu-dev \
  libmcrypt-dev \
  libmemcached-dev \
  libpq-dev \
  libxml2-dev \
  && rm -rf /var/lib/apt/lists/*

RUN debMultiarch="$(dpkg-architecture --query DEB_BUILD_MULTIARCH)" \
  && docker-php-ext-install intl mbstring mcrypt mysqli opcache pdo_mysql pdo_pgsql pgsql zip pcntl

# set PHP.ini settings
RUN { \
  echo 'opcache.enable=1'; \
  echo 'opcache.enable_cli=1'; \
  echo 'opcache.interned_strings_buffer=8'; \
  echo 'opcache.max_accelerated_files=10000'; \
  echo 'opcache.memory_consumption=128'; \
  echo 'opcache.save_comments=1'; \
  echo 'opcache.revalidate_freq=1'; \
  } > /usr/local/etc/php/conf.d/opcache-recommended.ini

ENV ROUNDCUBE_VERSION 1.3.0

RUN curl -fsSL -o roundcube.tar.gz \
    "https://github.com/roundcube/roundcubemail/releases/download/${ROUNDCUBE_VERSION}/roundcubemail-${ROUNDCUBE_VERSION}-complete.tar.gz" \
 && curl -fsSL -o roundcube.tar.gz.asc \
    "https://github.com/roundcube/roundcubemail/releases/download/${ROUNDCUBE_VERSION}/roundcubemail-${ROUNDCUBE_VERSION}-complete.tar.gz.asc" \
 && export GNUPGHOME="$(mktemp -d)" \
# gpg key from https://roundcube.net/download/roundcube.asc
 && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys F3E4C04BB3DB5D4215C45F7F5AB2BAA141C4F7D5 \
 && gpg --batch --verify roundcube.tar.gz.asc roundcube.tar.gz \
 && rm -r "$GNUPGHOME" roundcube.tar.gz.asc \
 && tar -xf roundcube.tar.gz -C /var/www \
 && rm -rf /var/www/html \
 && ln -sf /var/www/roundcubemail-${ROUNDCUBE_VERSION} /var/www/html \
 && chown -R root:www-data /var/www/html/

VOLUME /var/www/html/config

CMD ["php-fpm"]
