

## Sensors and Actors communication

There should be a way to react on the metrics. Start a pump, open a valve or some other actions.


## Actors hardware

- relay
- valve
- micro controlller


## Variants

### 433 MHz communication

- Needs special software for the actor
- Needs additional hardware for sender and receiver
	- 433 MHz sender
	- 433 MHz receiver
	- Cheap microcontroller for the actor (ESP-01, ESP-8266)


### 2.4 GHz WiFi  communication

- Needs a WifiRouter and special software for the actor


### 2.4 GHz Bluetooth communication

-  Needs additional hardware for receiver
	- ESP32 microcontroller for the actor
- Pros
	- No additional hardware for communication needed
- Cons
	- range
