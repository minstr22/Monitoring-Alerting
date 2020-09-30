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

![Grafana Dashboard](https://raw.githubusercontent.com/minstr22/Monitoring-Alerting/master/images/Dashboard1.png)

## Alerting With Discord
First we must Add Discord Notification channel
* Click the `Alert` Menu at the top left corner (looks like a bell)
* Click `Notification channels`
* Click the green button `Add channel`
* Choose type `Discord`
* Insert Webhook `Webhook URL`
![Alerts](https://raw.githubusercontent.com/minstr22/Monitoring-Alerting/master/images/Notification-discord.png)

## Alerting With Telegram
First we must Add Telegram Notification channel
* Click the `Alert` Menu at the top left corner (looks like a bell)
* Click `Notification channels`
* Click the green button `Add channel`
* Choose type `Telegram`
* Insert Your Telegram BOT `BOT API Token`
* Insert Your Telegram Group ID (where you want to get alerts) `Chat ID`
![Alerts](https://raw.githubusercontent.com/minstr22/Monitoring-Alerting/master/images/notification-telegram.png)


# Troubleshooting

It appears some people have reported no data appearing in Grafana. If this is happening to you be sure to check the time range being queried within Grafana to ensure it is using Today's date with current time.

## Mac Users

The node-exporter does not run the same as Mac and Linux. Node-Exporter is not designed to run on Mac and in fact cannot collect metrics from the Mac OS due to the differences between Mac and Linux OS's. 
