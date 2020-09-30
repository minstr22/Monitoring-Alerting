# Monitoring-Alerting With Prometheus And Grafana
## A Prometheus & Grafana docker-compose stack
Here's a quick manual to start-up a [Prometheus](http://prometheus.io/) stack containing Prometheus, Grafana and Node scraper to monitor your Docker infrastructure. 

## Pre-requisites
Before we get started installing the Prometheus stack. Ensure you install the latest version of docker and [docker-compose](https://docs.docker.com/compose/install/) on your Docker host machine.

# Installation & Configuration
Clone the project locally to your Docker host.

If you would like to change which targets should be monitored or make configuration changes edit the [/prometheus/prometheus.yml](prometheus/prometheus.yml) file. The targets section is where you define what should be monitored by Prometheus. The names defined in this file are actually sourced from the service name in the docker-compose file. If you wish to change names of the services you can add the "container_name" parameter in the `docker-compose.yml` file.

Once configurations are done let's start it up. From the /Monitoring-Alerting project directory run the following command:

    $ sudo mkdir -p /opt/grafana/data && chmod 775 /opt/grafana/data
    $ sudo mkdir -p /opt/prometheus/data && chmod 775 /opt/prometheus/data
    $ docker-compose up -d
The Grafana Dashboard is now accessible via: `http://<Host IP Address>` for example http://192.168.10.1

Here's the Dashboard Template
![Grafana Dashboard](https://raw.githubusercontent.com/minstr22/Monitoring-Alerting/master/Dashboard.png)
