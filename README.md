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
Default all configuration:
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

## Concepts
***Prometheus Architecture***

![Prometheus][]

***Docker Host Dashboard***

![Host][]

The Docker Host Dashboard shows key metrics for monitoring the resource usage of your server:

* Server uptime, CPU idle percent, number of CPU cores, available memory, swap and storage
* System load average graph, running and blocked by IO processes graph, interrupts graph
* CPU usage graph by mode (guest, idle, iowait, irq, nice, softirq, steal, system, user)
* Memory usage graph by distribution (used, free, buffers, cached)
* IO usage graph (read Bps, read Bps and IO time)
* Network usage graph by device (inbound Bps, Outbound Bps)
* Swap usage and activity graphs

***Docker Containers Dashboard***

![Containers][]

The Docker Containers Dashboard shows key metrics for monitoring running containers:

* Total containers CPU load, memory and storage usage
* Running containers graph, system load graph, IO usage graph
* Container CPU usage graph
* Container memory usage graph
* Container cached memory usage graph
* Container network inbound usage graph
* Container network outbound usage graph

Note that this dashboard doesn't show the containers that are part of the monitoring stack.

***Monitor Services Dashboard***

![Monitor Services][]

The Monitor Services Dashboard shows key metrics for monitoring the containers that make up the monitoring stack:

* Prometheus container uptime, monitoring stack total memory usage, Prometheus local storage memory chunks and series
* Container CPU usage graph
* Container memory usage graph
* Prometheus chunks to persist and persistence urgency graphs
* Prometheus chunks ops and checkpoint duration graphs
* Prometheus samples ingested rate, target scrapes and scrape duration graphs
* Prometheus HTTP requests graph
* Prometheus alerts graph

***Setup Alerting***

![Slack Notifications][]

The notification receivers can be configured in [alertmanager/config.yml][] file.

To receive alerts via Slack you need to make a custom integration by choose ***incoming web hooks*** in your Slack team app page.
You can find more details on setting up Slack integration [here][].

Copy the Slack Webhook URL into the ***api_url*** field and specify a Slack ***channel***.

```yaml
route:
    receiver: 'slack'

receivers:
    - name: 'slack'
      slack_configs:
          - send_resolved: true
            text: "{{ .CommonAnnotations.description }}"
            username: 'Prometheus'
            channel: '#<channel>'
            api_url: 'https://hooks.slack.com/services/<webhook-id>'
```

## How To Run?
* Clone this repository
  ```
  git clone git@github.com:nfndp/nfndp-docker.git
  ```
* Open your terminal then go to `nfndp-docker` folder
* Type: `./run.sh` or `/bin/sh ./run.sh`

## Running Container

***Docker Portainer***

* Create credential access:
```
username: laradock
password: password
```
* Select local containers

![Portainer][]

***Running in browser***
* Grafana: [localhost:8120](http://localhost:8120)
* NodeExporter: [localhost:9306](http://localhost:9306)
* Prometheus: [localhost:9307](http://localhost:9307)
* Caddy:
  - [localhost:9301](http://localhost:9301)
  - [localhost:9302](http://localhost:9302)
  - [localhost:9303](http://localhost:9303)
  - [localhost:9304](http://localhost:9304)
* cAdvisor: [localhost:9305](http://localhost:9305)
* Redis: [localhost:8152](http://localhost:8152)
* PostgreSQL: [localhost:8146](http://localhost:8146)
* Pushgateway: [localhost:9308](http://localhost:9308)

[laradock]:https://github.com/laradock/laradock
[Prometheus]:https://camo.githubusercontent.com/7cc17b981938e40974542fbfa9c34172fd92eccd/68747470733a2f2f63646e2e7261776769742e636f6d2f70726f6d6574686575732f70726f6d6574686575732f633334323537643036396336333036383564613335626365663038343633326666643564363230392f646f63756d656e746174696f6e2f696d616765732f6172636869746563747572652e737667
[Host]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/docs/grafana_docker_host.png
[Containers]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/docs/grafana_docker_containers.png
[Monitor Services]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/docs/grafana_prometheus.png
[Slack Notifications]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/docs/slack_notifications.png
[alertmanager/config.yml]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/config/alertmanager/config.yml
[here]:http://www.robustperception.io/using-slack-with-the-alertmanager/
[Portainer]:https://raw.githubusercontent.com/nfndp/nfndp-docker/master/docs/portainer.png