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
new window.plugins.mqtt({
            uri: MQTT_URI,
            keepAliveInterval: 120,
            clientId: MQTT_CLIENT_ID,
            reportConnectionStatus: false,
            reconnectDelay: [1000, 5000, 10000, -1]
        });
        btc.connect();

var connection = new window.plugins.mqtt({
    uri: 'ws://192.168.2.107:8080',
    keepAliveInterval: 120,
    clientId: 'BeeToo_MQTT',
    reportConnectionStatus: true,
    reconnectDelay: [1000, 5000, 10000, -1] //three tries to reconnect will take place. If -1 met, then reconnect process will stop.
});
connection.on('connected', function () {
    connection.subscribe('/russia/moscow/beetoo_status', {qos: 2});
    connection.publish('/russia/moscow/beetoo', 'hi, gyus!', {qos: 1, retained: true});
    connection.on('/russia/moscow/beetoo_status', function (value) {
        console.log('Yay! Value is: ' + value);
    });
});

connection.connect();
```

[The MIT License (MIT)](http://www.opensource.org/licenses/mit-license.html)