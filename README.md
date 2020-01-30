# VibrationSensor
Vibration Sensor using NodeMCU and Tasmota

# Parts
* 1 x SW-420 NC Type Vibration Sensor Module Vibration Switch
* 1 x NodeMCU V3
* 3 x Dupont Female to Female cables

# Instructions
* Flash latest release Tasmota to Nodemcu using Tasmotizer - https://github.com/tasmota/tasmotizer
* Connect dupont cables from NodeMCU to SW-420 as below
![Image description](https://imgur.com/ErQPBrk)
* Connect to NodeMCU AP (Tasmota-XXXX)
* Connect NodeMCU to your WAP and find it's DHCP IP
* Hit the config page of the NodeMCU
* Switch the module type to Generic
* Paste below Template into the "Template" section of "Configure Other"
  * {"NAME":"Generic","GPIO":[255,255,255,255,255,255,255,255,255,255,255,255,255],"FLAG":15,"BASE":18}
  

