# Using Node-RED in SCADABR via Modbus

In this tutorial I will explain how to integrate Node-RED via Modbus in a SCADA system, and how read and write values using simple HTTP requests.


## Environment 

For this test I am using the SCADA in a PC and Node-Red installed in a Raspberry Pi. I am using also a Modbus/MQTT board to get data of temperature and so on. You can replace it for creating a virtual dataset and virtual datapoints in ScadaBR.


### Versions
item | version | description
---|---|---|
ScadaBR | 1.2 | Supervisory Control and Data Acquisition
Node-RED | 2.0.6 | Programming Tool for API, Software and Hardware
node-red-contrib-modbus | 5.14.1 | Module to support Modbus inside Node-RED
NodeJS | 14.17.6 | Javascript for backend

### Downloads and documentation

* [ScadaBR](https://github.com/ScadaBR/ScadaBR/releases)
* [Node-RED running on Raspberry Pi](https://nodered.org/docs/getting-started/raspberrypi)
* [node-red-contrib-modbus](https://flows.nodered.org/node/node-red-contrib-modbus)
* [JE03 - portuguese](https://www.bintechnology.com.br/connectioje03)


## Configuring ScadaBR

The ScadaBR will be two datapoints, one for Node-RED and another one to JE03 board, I've created some point links that I will explain later.



### JR03 board

Click in Datasource icon ![Data Source Icon](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/01_DataSourceIcon.png) and click in *Add*, create a Data Source as below, replacing IP address for localhost or another one.

![Data Source JE03](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/02_DataSourceJE03.png) 


Now create the datapoints for RSSI, Temperatura (Temperature) and Umidade (humidity). 

![Datapoints JE03](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/03_Datapoints_JE03.png) 

Do not forget to enable the Data source and the datapoints

#### RSSI datapoint

![Datapoint RSSI](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/04_Datapoint_RSSI.png) 


#### Temperature datapoint

![Datapoint Temperature](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/05_Datapoint_Temperature.png) 


#### Humidity datapoint

![Datapoint Humidity](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/06_Datapoint_Humidity.png) 


