# esphome-marstek-venus-rs485

Standalone ESPHome-based controller for **Marstek Venus E 2.0** over RS485 (ESP32).

## Overview

The Venus E 2.0 often suffers from unstable Wi-Fi, making direct integration with Home Assistant unreliable.  
This project uses an ESP32 running ESPHome to control the device independently, with grid data provided via MQTT.

## References

- https://gathering.tweakers.net/forum/list_messages/2282240 (wiring)
- https://github.com/Superduper1969/MarstekVenus-LilygoRS485 (Modbus readout)
- https://du.nkel.dev/blog/2026-01-11_marstek-battery-homeassistant/ (control loop)

## Hardware

- ESP32 Dev Kit  
- MAX485 module  

## Wiring

![Wiring](img/Wiring.png)

## Current Controls
<p align="center">
  <img src="img/Screen1.png" alt="Web Interface" width="400">
  <img src="img/Screen2.png" alt="Web Interface" width="400">
</p>
## Configuration

The setup expects a single MQTT topic providing grid power data:

- **Grid power > 0** → battery will discharges  
- **Grid power < 0** → battery will charge  

Inverter efficiency values are reported as follows:

- **Negative values** → battery is charging  
- **Positive values** → battery is discharging  

## Notes

- The discharge power restriction must be configured via the official app. After initial setup, the app is no longer required.  
- The factory reset button has not yet been tested.
- Grid data from a Hichi meter can be fetched every second using a Tasmota script, for example.

```tasmota
    >D
    MQT = "Hichi"
    >B
    =>sensor53 r
    >M
    <YOUR M Section for the SML>
    >S
    =>publish %MQT%/Grid %4sml[1]%
``` 

## Changelog

 - Rewrite of yaml to ensure compatibility with ESPHome 2026.9.1 and later
 
 - The **Auto Mode** web interface includes two additional settings:
   - **Prevent Full Charge Before 14:00**: Enables the optional charging limit (disabled by default).
   - **SOC Limit Before 14:00**: Maximum SOC allowed by automatic charging before 14:00 (default: 90%, configurable from 50% to 99%).
   
This feature affects **ESPHome automatic mode only**, not manual commands or other external controllers.

## ToDo

- Add a logic level shifter to reduce ESP32 RX/TX voltage to 3.3V
