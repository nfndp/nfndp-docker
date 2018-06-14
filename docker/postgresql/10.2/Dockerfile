ARG POSTGRES_VERSION=10.2
FROM postgres:${POSTGRES_VERSION}

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

ENV POSTGRES_ROOT_PASSWORD="password" \
    POSTGRES_ROOT_HOST="localhost" \
    POSTGRES_DATABASE="laradock_postgresql" \
    POSTGRES_USER="laradock" \
    POSTGRES_PASSWORD="password" \
    PGDATA="/var/lib/postgresql/data"

VOLUME /var/lib/postgresql/data

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod 777 /usr/local/bin/docker-entrypoint.sh
RUN ln -sf usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
