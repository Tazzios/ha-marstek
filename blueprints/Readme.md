

# Marstek X Range OM Blueprint 
This Home Assistant automation controls Marstek batteries according to a **grid sensor**, managing **charging, discharging, and load balancing** across multiple batteries. It ensures that batteries operate efficiently within set limits and adjusts setpoint range dynamically based on grid consumption, battery SOC, and optional offsets. But it can also be used to normal load or unload your batteries. 
Based on the work of PimDoos: [HA Sessy Examples](https://github.com/PimDoos/ha-sessy-examples/tree/main)  

> **XOM** stands for **X on the Meter**, an alternative to NOM (which stands for Nul op de Meter).

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FTazzios%2Fha-marstek%2Fblob%2Fmain%2Fblueprints%2Fmarstek%2520x%2520range%2520om%2520blueprint.yaml)

## Key Features
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)    
- Rotates by priority template or  Keep SOC`s within 10% of each other option to ensure equal usage over time.  
- Set target range, create a deadband.  
- Minimum and maximum power option.
- Smooth transitions, minimum and maximum different in setpoint changes.
- Smooth transitions, Smoothing factor above adjustable level.
- Smooth transitions, seperate smoothing factor when passing zero.
- Start condition, Set a start condition before the script is allowed to run
- Setpoint template, Do you not want to follow the grid and do something custom?   


## Requirements
 Easy
- Marstek venus with the Local API enabl (modbus over ethernet)
- HA integration [ marstek venus modbus](https://github.com/ViperRNMC/marstek_venus_modbus/tree/main)
  - do not forget to enabled the neccesary entities mentioned below. 

Oldway
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
   
<img width="1044"  alt="Marstek XOM 2 0" src="https://github.com/user-attachments/assets/0f1e73fd-308e-4ece-9f8b-b71fc2fe4a7a" />

