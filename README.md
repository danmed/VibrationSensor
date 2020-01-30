# VibrationSensor
Vibration Sensor using NodeMCU and Tasmota

# Parts
* 1 x SW-420 NC Type Vibration Sensor Module Vibration Switch
* 1 x NodeMCU V3
* 3 x Dupont Female to Female cables

# Instructions
* Flash latest release Tasmota to Nodemcu using Tasmotizer - https://github.com/tasmota/tasmotizer
* Connect dupont cables from NodeMCU to SW-420 as below
![Image description](https://i.imgur.com/ErQPBrk.png)
* Connect to NodeMCU AP (Tasmota-XXXX)
* Connect NodeMCU to your WAP and find it's DHCP IP
* Hit the config page of the NodeMCU
* Switch the module type to Generic
* Set up MQTT and the Friendly Name
* Paste below Template into the "Template" section of "Configure Other"
  * ```{"NAME":"Generic","GPIO":[255,255,255,255,255,255,255,255,255,255,255,255,255],"FLAG":15,"BASE":18}```
  
# Rule
When this is activated it toggles instantly between motion and no motion.. To counter act that, you need to set up a rule to have it dish out an MQTT topic which stays on for a specified duration. Alter the 180 in the below rule to your spec (seconds) : 

```SwitchMode1 1
SwitchTopic 0
Rule1 on switch1#state=1 do backlog publish stat/%topic%/motion ON; RuleTimer1 180 endon on Rules#Timer=1 do publish stat/%topic%/motion OFF endon
Rule1 1
```

Now you will have an MQTT Topic stat/%topic%/motion which flicks ON and then 3 minutes later flicks to OFF.

# Home Assistant YAML

```YAML
- platform: mqtt
  name: "Motion"
  state_topic: stat/tasmota_topic/motion
  payload_on: "ON"
  payload_off: "OFF"
  device_class: motion
```
