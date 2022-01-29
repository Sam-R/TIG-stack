# TIG Stack
## mosquitto, telegraf, influxdb, grafana

This project is designed to work along side sensors on deviced such as the arduino and esp8266 modules. It is the "hub" for sensor data transmitted via other devices using MQTT.

It includes:
* Mosquitto message broker
* Telegraf message formatter
* InfluxDB for data storage
* Grafana for information display/dashboards

It is currently a work in progress, however should work as is.


### Usage:

clone this repository and from it's directory run `docker-compose up -d`

To generate credentials (including the default ones), drop into the mosquitto container shell
```
docker-compose exec mosquitto sh
```

and then run the password tool
```
mosquitto_passwd -c /mosquitto/config/acl mqttuser
```

You'll be prompted for a password. Once entered, you'll need to restart the docker stack:

```
docker-compose down; docker-compose up -d
```

You can customise the credentials for the mosquitto instance, but remember to update other config files (such as telegraf). Also note this is plaintext, more secure options are available but not covered with this sample project.

Setup MQTT on your sensors or other devices and have them point to the docker host (ports should be default). Use the `.docker/telegraf/telegraf.conf` file to define "Topics" you want to subscribe to.

Use grafana with the influx DB datasource and create a dashboard against your topics

![Grafana Chart Queries](screenshots/grafana_queries.png)
