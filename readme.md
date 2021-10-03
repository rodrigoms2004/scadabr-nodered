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

---

## Configuring ScadaBR

The ScadaBR will be two datapoints, one for Node-RED and another one to JE03 board, I've created some point links that I will explain later.


[ScadaBR](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/scadabr/readme.md)


## Configuring Node-RED

Setup for Node-RED