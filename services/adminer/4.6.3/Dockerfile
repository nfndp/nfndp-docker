ARG ADMINER_VERSION=4.6.3
FROM adminer:${ADMINER_VERSION}

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

#####################################
# SQL SERVER:
#####################################
USER root
ARG INSTALL_MSSQL=false
ENV INSTALL_MSSQL=${INSTALL_MSSQL}
RUN if [ ${INSTALL_MSSQL} = true ]; then \
  set -xe \
  && apk --update add --no-cache --virtual .phpize-deps $PHPIZE_DEPS unixodbc unixodbc-dev \
  && pecl channel-update pecl.php.net \
  && pecl install pdo_sqlsrv-4.1.8preview sqlsrv-4.1.8preview \
  && echo "extension=sqlsrv.so" > /usr/local/etc/php/conf.d/20-sqlsrv.ini \
  && echo "extension=pdo_sqlsrv.so" > /usr/local/etc/php/conf.d/20-pdo_sqlsrv.ini \
;fi

COPY rootfs/ /
RUN chown -R adminer:adminer /var/www/html

USER adminer

# Add volume for sessions to allow session persistence
VOLUME /sessions

# We expose Adminer on port 8080 (Adminer's default)
EXPOSE 8080
