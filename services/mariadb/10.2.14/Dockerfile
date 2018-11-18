ARG MARIADB_VERSION=10.2.14
FROM mariadb:${MARIADB_VERSION}

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

ENV MYSQL_ROOT_PASSWORD="password" \
    MYSQL_ROOT_HOST="mariadb" \
    MYSQL_DATABASE="laradock_mariadb" \
    MYSQL_USER="laradock" \
    MYSQL_PASSWORD="password"

VOLUME /var/lib/mysql

COPY ./docker-entrypoint.sh /usr/local/bin/
COPY ./healthycheck.sh /healthycheck.sh
RUN touch /healthycheck.cnf && chmod 777 /healthycheck.cnf
RUN touch /mysql-init-complete && chmod 777 /mysql-init-complete
RUN ln -sf usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat

ENTRYPOINT ["docker-entrypoint.sh"]

HEALTHCHECK CMD /healthycheck.sh

EXPOSE 3306
CMD ["mysqld"]