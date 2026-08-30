# Marstek X Range OM Blueprint 
This Home Assistant automation controls Marstek batteries according to a **grid sensor**, managing **charging, discharging, and load balancing** across multiple batteries. It ensures that batteries operate efficiently within set limits and adjusts setpoint range dynamically based on grid consumption, battery SOC, and optional offsets. But it can also be setup to load or unload your batteries. 

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FTazzios%2Fha-marstek%2Fblob%2Fmain%2Fblueprints%2Fmarstek%2520x%2520range%2520om%2520blueprint.yaml)

[Documentation: Getting started and settings overview](https://github.com/Tazzios/ha-marstek/blob/main/blueprints/Documentation.md)

## Features
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)    
- Keep SOC`s within x% of each other option to ensure equal usage over time or Rotates by priority template.  
- Set grid target range, create a deadband.
- Setpoint template, Do you not want to follow the grid and do something custom?   
- Minimum and maximum power option.
- Smooth transitions, minimum and maximum different in setpoint changes.
- Adjustable Smoothing factors; when passing zero, above a level and when near grid targets.
- Start condition, Set a start condition before the script is allowed to run
- Stop action, When the start condition is not met do something else instead.

## Getting your Marstek in Home assistant
If you do not have the Marstek in Home assistant yet.

Easy way  
1. Marstek venus with firmware that supports TCP modbus and connected ethernet cable (not wifi)
2. HA integration [ marstek venus modbus](https://github.com/ViperRNMC/marstek_venus_modbus/tree/main) or [Marstek Venus Energy Manager](https://github.com/ffunes/Marstek-Venus-Energy-Manager)
3. Enabled the neccesary entities mentioned below. 

Old way
- Marstek Venus E v1,v2 or v3.
- Supported ESPHome configurations
  - [fonske/MarstekVenus-LilygoRS485](https://github.com/fonske/MarstekVenus-LilygoRS485)  
  - [onske/MarstekVenus-M5stackRS485](https://github.com/fonske/MarstekVenus-M5stackRS485)  
  - [Superduper1969/MarstekVenus-LilygoRS485](https://github.com/Superduper1969/MarstekVenus-LilygoRS485)
    
or other ESPHOME software that has the following entities endig with in home assistant:
  - `rs485_control_mode`  
  - `forcible_charge_discharge`  
  - `ac_power`  
  - `forcible_charge_power`  
  - `forcible_discharge_power`  
  - `state_of_charge`

## Screenshot 
<img width="979" height="3138" alt="afbeelding" src="https://github.com/user-attachments/assets/1387cf39-a400-4808-aad3-6f2eeb07db89" />

