ARG PGADMIN4_VERSION=3.0
FROM dpage/pgadmin4:${PGADMIN4_VERSION}

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

ENV PGADMIN_DEFAULT_EMAIL="laradock@laradock.io" \
    PGADMIN_DEFAULT_PASSWORD="password"

RUN mkdir -p /sessions

EXPOSE 80

VOLUME ["/sessions"]