# esphome-marstek-venus-rs485
Standalone ESPHome-based controller for Marstek Venus E 2.0 over RS485 (ESP32).

Based on:  
https://gathering.tweakers.net/forum/list_messages/2282240 (wiring)  
https://github.com/Superduper1969/MarstekVenus-LilygoRS485 (modbus readout)  
https://du.nkel.dev/blog/2026-01-11_marstek-battery-homeassistant/ (control loop)  
  
Venus E 2.0 often has unstable Wi-Fi, making Home Assistant control unreliable. This project uses ESPHome with a standalone ESP32 to control the Marstek device, fetching grid data via MQTT.  
  
Hardware:  
ESP32 Dev Kit  
MAX485 Module  

Wiring:  
  
![Wiring](img/Wiring.png)

Current controls:  
  
![Screen1](img/Screen1.png) ![Screen2](img/Screen2.png)

ToDos:  
Optimize modbus timing  
Add Reset and Factory Reset button  
Include logic level shifter to reduce ESP32 RX and TX voltage to 3.3V  
