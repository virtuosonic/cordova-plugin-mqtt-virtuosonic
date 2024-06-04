## Pure JavaScript MQTT client library. Wrapper for paho.js by [virtuosonic](http://machines.virtuosonic-sdc.com) ##

### Preamble 
This is a fork of the plugin [cordova-plugin-mqtt-pahojs](https://github.com/estbeetoo/cordova-plugin-mqtt-pahojs) that break compatibility by changing the api.

### Installation

For Cordova CLI users:

```
cordova plugin add https://github.com/virtuosonic/cordova-plugin-mqtt-virtuosonic.git
```

### Usage example

``` javascript

const connection = new window.plugins.mqtt({
	uri: 'ws://192.168.2.107:8080',
	keepAliveInterval: 120,
	clientId: 'BestClient_MQTT',
	reportConnectionStatus: true,
	reconnectDelay: [1000, 5000, 10000, -1] //three tries to reconnect will take place. If -1 met, then reconnect process will stop.
});

connection.on('connected', function () {
	connection.subscribe('oven/temperature', {qos: 2});
	connection.subscribe('oven/cakes/count', {qos: 2});
	connection.publish('alarms/firealert', 'hi, guys!', {qos: 1, retained: true});
	connection.on('message', function (msg) {
		switch ( msg.destinationName)
		{
			case 'oven/temperature':
				const celsius = msg.payloadFloat;
				console.log(`oven temperature is ${celsius} degrees`);
				break;
			case 'oven/cakes/count':
				const count = msg.playloadUint32;
				console.log(`oven has ${count} cakes`);
				break;
		}
    });
});

connection.connect();
```

[The MIT License (MIT)](http://www.opensource.org/licenses/mit-license.html)