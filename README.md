# Monitoring-Alerting With Prometheus And Grafana
## A Prometheus & Grafana docker-compose stack
Here's a quick manual to start-up a [Prometheus](http://prometheus.io/) stack containing Prometheus, Grafana and Node scraper to monitor your Docker infrastructure. 

## Pre-requisites
Before we get started installing the Prometheus stack. Ensure you install the latest version of docker and [docker-compose](https://docs.docker.com/compose/install/) on your Docker host machine.

# Installation & Configuration
Clone the project locally to your Docker host.

If you would like to change which targets should be monitored or make configuration changes edit the [/prometheus/prometheus.yml](prometheus/prometheus.yml) file. The targets section is where you define what should be monitored by Prometheus. The names defined in this file are actually sourced from the service name in the docker-compose file. If you wish to change names of the services you can add the "container_name" parameter in the `docker-compose.yml` file.

Once configurations are done let's start it up. From the /Monitoring-Alerting project directory run the following command:

    $ sudo mkdir -p /opt/grafana/data && sudo chmod -R 777 /opt/grafana/data
    $ sudo mkdir -p /opt/prometheus/data && sudo chmod -R777 /opt/prometheus/data
    $ docker-compose up -d
The Grafana Dashboard is now accessible via: `http://<Host IP Address>` for example http://192.168.10.1

Here's the Dashboard Template:

![Grafana Dashboard](https://raw.githubusercontent.com/minstr22/Monitoring-Alerting/master/Dashboard.png)

## Alerting With
Alerting has been added to the stack with Slack integration. 2 Alerts have been added and are managed

Alerts              - `prometheus/alert.rules`
Slack configuration - `alertmanager/config.yml`

The Slack configuration requires to build a custom integration.
* Open your slack team in your browser `https://<your-slack-team>.slack.com/apps`
* Click build in the upper right corner
* Choose Incoming Web Hooks link under Send Messages
* Click on the "incoming webhook integration" link
* Select which channel
* Click on Add Incoming WebHooks integration
* Copy the Webhook URL into the `alertmanager/config.yml` URL section
* Fill in Slack username and channel
