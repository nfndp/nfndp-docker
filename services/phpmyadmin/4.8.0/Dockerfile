ARG PHP_VERSION=7.2.4
ARG ALPINE_VERSION=3.7
FROM php:${PHP_VERSION}-fpm-alpine${ALPINE_VERSION}

# ================================================================================================
#  Inspiration: Docker Framework (https://github.com/zeroc0d3/docker-framework)
#               Dwi Fahni Denni <zeroc0d3.0912@gmail.com>
# ================================================================================================
#  Core Contributors:
#   - Mahmoud Zalt @mahmoudz
#   - Bo-Yi Wu @appleboy
#   - Philippe Trépanier @philtrep
#   - Mike Erickson @mikeerickson
#   - Dwi Fahni Denni @zeroc0d3
#   - Thor Erik @thorerik
#   - Winfried van Loon @winfried-van-loon
#   - TJ Miller @sixlive
#   - Yu-Lung Shao (Allen) @bestlong
#   - Milan Urukalo @urukalo
#   - Vince Chu @vwchu
#   - Huadong Zuo @zuohuadong
# ================================================================================================

MAINTAINER "Laradock Team <mahmoud@zalt.me>"

ENV PHPMYADMIN_VERSION=4.8.0
ENV URL=https://files.phpmyadmin.net/phpMyAdmin/${PHPMYADMIN_VERSION}/phpMyAdmin-${PHPMYADMIN_VERSION}-all-languages.tar.gz
LABEL version=$PHPMYADMIN_VERSION

ENV PMA_ARBITRARY="1"
ENV PMA_DB_ENGINE="mariadb"
ENV PMA_HOST="mariadb" \
    PMA_USER="laradock" \
    PMA_PASSWORD="password" \
    PMA_ROOT_PASSWORD="password"

ENV MYSQL_HOST=${PMA_DB_ENGINE} \
    MYSQL_USER=${PMA_USER} \
    MYSQL_PASSWORD=${PMA_PASSWORD} \
    MYSQL_ROOT_PASSWORD=${PMA_ROOT_PASSWORD}

RUN apk add --no-cache \
    nginx \
    supervisor

RUN set -ex; \
    \
    apk add --no-cache --virtual .build-deps \
        bzip2-dev \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxpm-dev \
    ; \
    \
    docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-webp-dir=/usr --with-png-dir=/usr --with-xpm-dir=/usr; \
    docker-php-ext-install bz2 gd mysqli opcache zip; \
    \
    runDeps="$( \
        scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
            | tr ',' '\n' \
            | sort -u \
            | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )"; \
    apk add --virtual .phpmyadmin-phpexts-rundeps $runDeps; \
    apk del .build-deps

COPY rootfs/ /
COPY ./run.sh /run.sh
RUN chmod u+rwx /run.sh

RUN set -ex; \
    \
    apk add --no-cache --virtual .fetch-deps \
        gnupg \
    ; \
    \
    export GNUPGHOME="$(mktemp -d)"; \
    export GPGKEY="3D06A59ECE730EB71B511C17CE752F178259BD92"; \
    curl --output phpMyAdmin.tar.gz --location $URL; \
    curl --output phpMyAdmin.tar.gz.asc --location $URL.asc; \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPGKEY" \
        || gpg --keyserver ipv4.pool.sks-keyservers.net --recv-keys "$GPGKEY" \
        || gpg --keyserver keys.gnupg.net --recv-keys "$GPGKEY" \
        || gpg --keyserver pgp.mit.edu --recv-keys "$GPGKEY" \
        || gpg --keyserver keyserver.pgp.com --recv-keys "$GPGKEY"; \
    gpg --batch --verify phpMyAdmin.tar.gz.asc phpMyAdmin.tar.gz; \
    rm -rf "$GNUPGHOME"; \
    tar xzf phpMyAdmin.tar.gz; \
    rm -f phpMyAdmin.tar.gz phpMyAdmin.tar.gz.asc; \
    mv phpMyAdmin-$PHPMYADMIN_VERSION-all-languages /www; \
    rm -rf /www/setup/ /www/examples/ /www/test/ /www/po/ /www/composer.json /www/RELEASE-DATE-$PHPMYADMIN_VERSION; \
    sed -i "s@define('CONFIG_DIR'.*@define('CONFIG_DIR', '/etc/phpmyadmin/');@" /www/libraries/vendor_config.php; \
    chown -R root:nobody /www; \
    find /www -type d -exec chmod 750 {} \; ; \
    find /www -type f -exec chmod 640 {} \; ; \
    apk del .fetch-deps

RUN mkdir /sessions \
    && mkdir -p /www/tmp \
    && chmod -R 777 /www/tmp

EXPOSE 80

ENTRYPOINT [ "/run.sh" ]
CMD ["phpmyadmin"]
