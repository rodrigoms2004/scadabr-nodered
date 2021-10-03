# ScadaBR setup

Follow this setup

## JR03 board datasource

Click in Datasource icon ![Data Source Icon](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/01_DataSourceIcon.png) and click in *Add*, create a Data Source as below, replacing IP address for localhost or another one.

![Data Source JE03](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/02_DataSourceJE03.png) 


Now create the datapoints for RSSI, Temperatura (Temperature) and Umidade (humidity). 

![Datapoints JE03](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/03_Datapoints_JE03.png) 

Do not forget to enable the Data source and the datapoints

### RSSI datapoint

![Datapoint RSSI](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/04_Datapoint_RSSI.png) 


### Temperature datapoint

![Datapoint Temperature](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/05_Datapoint_Temperature.png) 


### Humidity datapoint

![Datapoint Humidity](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/06_Datapoint_Humidity.png) 

---

## Node-RED datasource

Create the datasource 

![Data Source NodeRED](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/07_DataSourceNodeRED.png) 

An data point called distance

![Data Point Distance](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/08_Datapoint_Distance.png) 

And three data points for Celsius, Fahrenheit and Kelvin scales, same config but address and name.

![Data Point Temperature](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/09_Datapoint_Temperature.png) 

In the end we will have four datapoints

![Data Points](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/10_Datapoints.png) 

---

## Point links

Click in the icon of point links ![Point Links icon](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/11_Pointlink_icon.png) and create three point links associating JE03 temperature to the Node-RED datapoints. 

![Point links](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/12_Pointlinks.png) 

### Point link Kelvin

Converts temperature from celsius to Kelvin, where source point is the JE03 temperature datapoint returning the value to the Node-RED Kelvin temperature datapoint.

```
var temC;
var tempK;

tempC = source.value;
tempK = tempC + 273.15

return tempK
```

![Point link Kelvin](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/13_Pointlink_Kelvin.png) 

### Point link Fahrenheit

Converts temperature from celsius to Fahrenheit, where source point is the JE03 temperature datapoint returning the value to the Node-RED Fahrenheit temperature datapoint.

```
var temC;
var tempF;

tempC = source.value;
tempF = (tempC * 9/5) + 32;

return tempF
```

![Point link Fahrenheit](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/14_Pointlink_Fahrenheit.png) 

### Point link Celsius

Now its only sends temperature from a datapoint to another.

```
return source.value;
```

![Point link Celsius](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/15_Pointlink_Celsius.png) 

---

## Watch list

Click in Watch list icon and create a watch list name *nodered* as below:

![Watch List](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/scadabr/16_WatchList.png) 

---

