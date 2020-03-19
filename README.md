# docker-compose-mqtt-tig

Docker compose repo with MQTT, Telegraf, InfluxDB and Grafana.

### Prerequisites

In order to use this compose file (docker-compose.yml) you must have:

1. docker [https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/)
2. docker-compose [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
3. docker-compose-letsencrypt-nginx-proxy-companion [https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion](https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion)


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
    cp etc/grafana/grafana.ini.dist etc/grafana/grafana.ini


    # Start services
    sudo docker-compose up -d

    # Copy the configuration file to the container
    sudo docker cp $(pwd)/etc/influxdb/influxdb.conf $(sudo docker-compose ps -q influxdb):/etc/influxdb/influxdb.conf
    sudo docker cp $(pwd)/etc/telegraf/telegraf.conf $(sudo docker-compose ps -q telegraf):/etc/telegraf/telegraf.conf
    sudo docker cp -avr $(pwd)/etc/telegraf/telegraf.d $(sudo docker-compose ps -q telegraf):/etc/telegraf
    ```

    create the file passwd in  /mosquitto/config/ in the mqtt contanier
    create a copy of the grafana and mosquitto config already present in the containers
    
     ```sh
    sudo docker cp $(pwd)/etc/mqtt/mosquitto.conf $(sudo docker-compose ps -q mqtt):mosquitto/config/mosquitto.conf
    sudo docker cp $(pwd)/etc/grafana/grafana.ini $(sudo docker-compose ps -q grafana):/etc/grafana/grafana.ini 
    
   
    give permissions to all db in flixbus e.g: GRANT READ ON mqtt_metrics TO grafana

    #Grafana Dashboard
    https://grafana.com/dashboards/1150
    https://grafana.com/dashboards/928

    # Restart the server to reload the configuration
    sudo docker-compose restart

    ```