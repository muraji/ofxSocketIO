# ofxSocketIO

### Description

`ofxSocketIO` is an ofxaddon that wraps [`socket.io-client-cpp](https://github.com/socketio/socket.io-client-cpp). **It is still under active development.**

### Installation

`ofxSocketIO` provides the compiled libraries for `osx` and `linux64` out of the box. If you have to compile `socket.io-client-cpp yourself`, follow the [installation](https://github.com/socketio/socket.io-client-cpp/blob/master/INSTALL.md) instructions.

##### TLS/SSL

`socket.io-client-cpp` compiles with SSL support by default. However, we had issues with certificates and thus removed the SSL support. **The provided libs (osx and linux64) does not support TLS/SSL**.

*FYI, we simply removed the `find_package(OpenSSL)` call in the `CMakeLists.txt`.*

### Usage

Take a look at our [example](https://github.com/soixantecircuits/ofxSocketIO/tree/master/example).

You'll need a [socket.io server](http://www.socket.io) to communicate with. (check out [our test server](https://github.com/soixantecircuits/ofxSocketIO/tree/master/example/script))

### API

#### ofxSocketIO

##### `setup(std::string& address)`
&rarr; Creates a websocket connection with the `address` remote.

##### `bindEvent(ofEvent<ofxSocketIOData&>& event, std::string eventName)`
&rarr; Binds an `ofEvent` to `string` trigger. Typically, you'd do:
```cpp
std::string eventName = "server-event";
socketIO.bindEvent(serverEvent, eventName);
ofAddListener(serverEvent, this, &ofApp::onServerEvent);

void ofApp::onServerEvent (ofxSocketIOData& data) {
  // Will be triggered when the server emits a "server-event" event
  // See the `ofxSocketIOData` API on how to use the `data` parameter here
}
```

##### `connectionEvent`
&rarr; An `ofEvent` triggered when the socket is connected to the server

##### `notifyEvent`
&rarr; An `ofEvent` triggered when the socket is connected, closed, errored, or when the socket is trying to reconnect. Comes with `std::string` status parameter.

##### `emit(std::string& eventName, std::string& data)`
&rarr; Emits an event with the specified event name and a **string parameter** (you'll have to cast your non-string datas).

##### `closeConnection()`
&rarr; Force closes the socket.

#### ofxSocketIOData

##### `getStringValue(std::string key)`
&rarr; Get the `std::string` value for the specified key.

##### `getIntValue(std::string key)`
&rarr; Get the `int` value for the specified key.

##### `getFloatValue(std::string key)`
&rarr; Get the `float` value for the specified key.

##### `getDoubleValue(std::string key)`
&rarr; Get the `double` value for the specified key.

##### `getBoolValue(std::string key)`
&rarr; Get the `bool` value for the specified key.


### Credits

`ofxSocketIO` is maintained by [Soixante circuits](http://www.soixantecircuits.fr).

It exists thanks to the great work of the [socket.io-client-cpp contributors](https://github.com/socketio/socket.io-client-cpp/graphs/contributors).

### License

[MIT](https://github.com/soixantecircuits/ofxSocketIO/blob/master/LICENSE)