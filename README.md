# NFNDP Docker

[![GitHub issues](https://img.shields.io/github/issues/nfndp/nfndp-docker.svg)](https://github.com/nfndp/nfndp-docker/issues) [![GitHub forks](https://img.shields.io/github/forks/nfndp/nfndp-docker.svg)](https://github.com/nfndp/nfndp-docker/network) [![GitHub stars](https://img.shields.io/github/stars/nfndp/nfndp-docker.svg)](https://github.com/nfndp/nfndp-docker/stargazers) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/nfndp/nfndp-docker/master/LICENSE)

NFN Design & Partnership Docker Tools, adopted from [laradock][].

## Containers
Docker container includes:
* consul
* adminer
* grafana
* mariadb
* mongodb
* mysql
* percona
* pgadmin
* phpmyadmin
* portainer
* postgresql
* prometheus
* redis

## Configuration
Default configuration:
* `username: laradock`
* `password: password`

## Monitoring Tools
* Prometheus (metrics database) `http://<host-ip>:9090`
* Prometheus-Pushgateway (push acceptor for ephemeral and batch jobs) `http://<host-ip>:9091`
* AlertManager (alerts management) `http://<host-ip>:9093`
* Grafana (visualize metrics) `http://<host-ip>:3000`
* NodeExporter (host metrics collector)
* cAdvisor (containers metrics collector)
* Caddy (reverse proxy and basic auth provider for prometheus and alertmanager)

[laradock]:https://github.com/laradock/laradock