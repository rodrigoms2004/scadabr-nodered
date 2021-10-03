# Node-red config

Import the config file to load this setup

![Node-RED](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/01_Node-RED.png)

You need to install node-red-contrib-modbus, check it in Menu>Manage Palette and tab Node

![Node-RED_modbus](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/02_Node-RED_modbus.png)

---

## Create a Modbus server

Using a Modbus Flex Server make it listen all address (0.0.0.0) in the TCP port 14502, Unit-Id 9 (In ScadaBR Unitid is the SlaveId of the Datapoints)

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/03_ModbusFlexServer.png)

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/04_ModbusFlexServerConfig.png)

---

## Reading temperatures from Scada


Create three Modbus Read nodes with a debug and a Modbus response for each one. They will receive temperature data from Node-RED datapoints configured in ScadaBR.

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/05_ReadingData.png)

For read Celsius setup as below

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/06_ReadCelsius.png)

For Kelvin and Fahrenheit just change Address to 10 and 15 respectively
