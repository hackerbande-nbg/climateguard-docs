# Table Overview

## device

keeps metadata per device
- name --> as displayed in app
- hardware_id --> for tracking the hardware configuration
- software_id --> for trackinhg firmware version
- latitude + longiture --> where it's located
- appeui / deveui / appkey --> for TTN registration
- ground_cover /height_above_ground / ... --> planned metadata regarding the location

## sensormessage

metadata regarding the physical messages in the TTN.
See also: https://www.thethingsnetwork.org/docs/lorawan/

## sensormetric

timestamps --> currently based on when it is read from MQTT
temperature / humidity / air_pressure --> readings from sensor
battery_voltage --> output from ESP
confirmed / consumed airtime / f_cnt / frequency --> lorawan data

## tag

meta table where specific tags can be stored, e.g. productive
linked via taglink tables

 
