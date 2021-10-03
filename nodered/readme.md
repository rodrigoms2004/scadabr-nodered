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


Create three Modbus Read nodes with a debug and a Modbus response for each one. They will receive temperature data from Node-RED datapoints configured in ScadaBR. For this config the poll rate is setup for every 1 second, but you can change it as you wish.

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/05_ReadingData.png)

For read Celsius setup as below

![Modbus Flex Server](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/06_ReadCelsius.png)

For Kelvin and Fahrenheit just change Address to 10 and 15 respectively

Now you are able to read all temperatures scales via modbus.

---

## Reading temperatures via HTTP GET request

Now using a browser we can read all temperature scales, simply make requests in the browser like: 

* Default (Celsius) HTTP GET http://localhost:1880/modbus/temperature
* Kelvin HTTP GET http://localhost:1880/modbus/temperature/k
* Fahrenheit HTTP GET http://localhost:1880/modbus/temperature/f

You will receive an array with one element, ok it is possible to improve it, but lets make the things simple for now.

![Read HTTP](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/07_ReadHTTP.png)

### Modbus node vs HTTP

For some reason modbus nodes like Getter, Flex Getter, Write and Flex Write don't forward http.request and http.response, causing a timeout because Http Response node is not able to respond the request. 

![Read HTTP](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/08_HttpResponse.png)

For this reason I've stored the initial http.req and http.res in the context of the flow when the request is made, then I can get it back in HTTP response.

![Read HTTP](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/09_Flow.png)

In the function **read** firts I store HTTP.req and HTTP.res in the variabe msgHttp

```
var msgHttp = {
    req: msg.req,
    res: msg.res
}
flow.set('msgHttp', msgHttp);
...

```

An use it in the function **HTTP Payload** with get flow context msgHttp and the payload from modbus (Getter or Write).

```
var { req, res } = flow.get('msgHttp') || {};

var newMsg = {
    payload: msg.payload,
    req, 
    res
}

return newMsg;
```

This funcion is connected to a Http Response node wich return HTTP code 200 in JSON format. It works for both Modbus Write and Modbus Getter nodes.

### Function read

After stores http data in the flow

```
var msgHttp = {
    req: msg.req,
    res: msg.res
}
flow.set('msgHttp', msgHttp);

```

Function **read** gets parameter scale if exists and returns the appropriate value

```
var { scale } = msg.req.params;

msg.payload = { 
    value: msg.payload,
    fc: 3, 
    unitid: 9, 
    address: 20, // datapoint Celsius
    quantity: 1,
    scale
};

if (scale == "k") {
    msg.payload['address'] = 10; // datapoint Kelvin
}

if (scale == "f") {
    msg.payload['address'] = 15; // datapoint Fahrenheit
}

return msg;
```

---

## Writing data via HTTP GET

We can write a number in the datapoint distance inside ScadaBR, remind yoursef that the aximum value of a 2 byte unsigned int is 65535, then we can write distance between 0 and 65535.


* Write distance HTTP GET http://localhost:1880/modbus/ultrasonico?distance=1234


![Write HTTP](https://github.com/rodrigoms2004/scadabr-nodered/blob/main/img/nodered/10_WriteHTTP.png)


### Function write

In function *write* we store the http request as we made in http read, check if the distance is in the boundaries, and send the data to the modbus flex write.  

```
var msgHttp = {
    req: msg.req,
    res: msg.res
};
flow.set('msgHttp', msgHttp);

var { distance } = msg.payload;

if (parseInt(distance) > 65535) {
    distance = 65535;
}

msg.payload = { 
    value: distance,
    fc: 6,
    unitid: 9,
    address: 5,
    quantity: 1
};

return msg;
```

---






