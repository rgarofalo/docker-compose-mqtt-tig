# docker-compose-mqtt-tig

Docker compose repo with MQTT, Telegraf, InfluxDB and Grafana.


### Getting started

1. Clone project :

    ```sh
    git clone https://github.com/rgarofalo/docker-compose-mqtt-tig.git
    ```

2. You could customize your settings before installation :

    Edit `.env` file

3. Install :

    ```sh
    # Copy the configuration file from the dist file
    cp etc/mqtt/mqtt.conf.dist etc/mqtt/mqtt.conf
    cp etc/telegraf/telegraf.conf.dist etc/telegraf/telegraf.conf
    cp etc/influxdb/influxdb.conf.dist etc/influxdb/influxdb.conf

    # Start services
    sudo docker-compose up -d

    # Copy the configuration file to the container
    sudo docker cp $(pwd)/etc/influxdb/influxdb.conf $(sudo docker-compose ps -q influxdb):/etc/influxdb/influxdb.conf
    sudo docker cp $(pwd)/etc/mqtt/mosquitto.conf $(sudo docker-compose ps -q mqtt):mosquitto/mosquitto.conf
    sudo docker cp $(pwd)/etc/telegraf/telegraf.conf $(sudo docker-compose ps -q telegraf):/etc/telegraf/telegraf.conf

    #Grafana Dashboard
    https://grafana.com/dashboards/1150
    https://grafana.com/dashboards/928

    # Restart the server to reload the configuration
    sudo docker-compose restart

    ```