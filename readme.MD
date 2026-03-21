# PFC modbus-server & node-red demo application

## 1. Documentation 

* Node-Red modbus contribution, tutorial video:</br>
https://stevesnoderedguide.com/modbus-writing-data

* Node-Red modbus contribution: `node-red-contrib-modbus`</br>
  https://flows.nodered.org/node/node-red-contrib-modbus

* WAGO fieldbus coupler manual 750-362</br>
  https://www.wago.com/wagoweb/documentation/750/eng_manu/coupler_controller/m07500362_xxxxxxxx_0en.pdf

* WAGO serial interface manual 750-1652</br>
  https://www.wago.com/wagoweb/documentation/750/ger_manu/modules/m07501652_00000000_0de.pdf

* WAGO IO-System product documentation</br>
  https://www.wago.com/wagoweb/documentation/index_d.htm

## 2. Installation

### 2.1 Connect the Controller to the Internet

Login the Web Based Management (WBM)

> Set a valid DNS-server

![DNS-setting](./img/image01.png)
</br></br>

> Set a valid time server (NTP-server)

![NTP-Settingr](img/image02.png)
</br></br>

> Activate IP Forwarding through multiple interfaces</br>

![NTP-Settingr](img/image03.png)
</br></br>

> Make sure the Domaine names are correctly solve</br>

    ping google.com
</br>

> Enables the controller to run Docker</br>

![Enable-Docker](img/image04.png)
</br></br>

### 2.2 Download and start "modbus server" Docker container

https://hub.docker.com/r/wagoautomation/pfc-modbus-server

*the container is downloaded automaticly:*
```
docker run -d \
--init \
--restart unless-stopped \
--privileged \
-p 502:502 \
--name=pfc-modbus-server \
-v /var/run/dbus/system_bus_socket:/var/run/dbus/system_bus_socket \
wagoautomation/pfc-modbus-server 
```

*Make sure to use original WAGO `armV7` images becouse the PFC200 have less memory capacity*

### 2.3 Download and start "node-red" Docker container

https://hub.docker.com/r/wagoautomation/node-red-cc100

*the container is downloaded automaticly*
```
docker run -d --name wago-node-red \
--restart unless-stopped \
-d --privileged=true --user=root \
-p 1880:1880 \
-v node_red_user_data:/data \
wagoautomation/node-red-cc100:1.0.0

```

*Make sure to use original WAGO `armV7` images becouse the PFC200 have less memory capacity*

### 2.3 install the node-red-contrib-modbus contribution

if necessery install node-red-contrib-modbus :
> `ALT+SHIFT+P` or `manage palette` menu:

![Install-Modbus-Contrib](img/image05.png)
</br></br>

## 3. Import the flows in the Node-red environement

* Open the Node-red UI within a Browser:</br>
  http://192.168.1.17:1880

  *the Container doesn't support HTTPs encrypted communication*

