ARG REDIS_VERSION=4.0
FROM redis:${REDIS_VERSION}-alpine

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

RUN mkdir -p /data && chown redis:redis /data
VOLUME /data
WORKDIR /data

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod 777 /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 6379
CMD ["redis-server"]