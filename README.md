# Huawei SUN2000 KTL L1 Inverter Modbus RTU to MQTT
Monitoring the Huawei SUN2000L KTL L1 inverter via Modbus RTU and publishing the values to MQTT

**What is this?**

This script allows to control a Huawei SUN2000L KTL L1 inverter via Modbus RTU and to publish the values in MQTT (for use in node-red, Home Assistant, OpenHab...).

This is the RTU version of my TCP project: https://github.com/ccorderor/huawei-sun2000-modbus-mqtt

I use a forked version of the HuaweiSolar library (https://gitlab.com/Emilv2/huawei-solar) from Emilv2. 

Finally, there is also the possibility to build a docker image and launch it in any environment.

A lot of information, code and knowledge extracted from:

- https://domotuto.com/conexion-del-inversor-fotovoltaico-huawei-sun2000-a-broker-mqtt-node-red/
- https://www.dropbox.com/s/9zaa1zexnr6cv60/detalles_modbus-tcp.py?dl=0
- https://community.home-assistant.io/t/integration-solar-inverter-huawei-2000l/132350/1

*Howto generate docker container*

First, download the code from this repo (you can either clone the repo or download the gzip file and extract it).
You should download it in the same computer you are going to run the container.

Then, you need to generate the docker image. Enter inside the code folder, and execute the following command:

```
docker build -t huawei-solar-rtu .
```

Once the docker image has been generated, you can use the following docker-compose service to initialize it:

```
 huawei-solar-rtu:
    container_name: huawei-solar-rtu
    restart: unless-stopped
    image: huawei-solar-rtu:latest
    user: root
    devices:
      - /dev/ttyUSB0:/dev/ttyUSB0
    environment:
      - INVERTER_PORT=/dev/ttyUSB0
      - MQTT_HOST=192.168.1.15
```

*Docker container*

![docker](https://raw.githubusercontent.com/ccorderor/huawei-sun2000-modbus-mqtt/main/images/huawei_docker.png)


*Node-red mqtt listeners*

![node-red](https://raw.githubusercontent.com/ccorderor/huawei-sun2000-modbus-mqtt/main/images/huawei_nodered.png)
