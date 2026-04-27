# Marstek X Range OM Blueprint 
This Home Assistant automation controls Marstek batteries according to a **grid sensor**, managing **charging, discharging, and load balancing** across multiple batteries. It ensures that batteries operate efficiently within set limits and adjusts setpoint range dynamically based on grid consumption, battery SOC, and optional offsets. But it can also be setup to load or unload your batteries. 

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FTazzios%2Fha-marstek%2Fblob%2Fmain%2Fblueprints%2Fmarstek%2520x%2520range%2520om%2520blueprint.yaml)

[Documentation: Getting started and settings overview](https://github.com/Tazzios/ha-marstek/edit/V2.0/blueprints/Documentation.md)

## Features
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)    
- Keep SOC`s within x% of each other option to ensure equal usage over time or Rotates by priority template.  
- Set grid target range, create a deadband.
- Setpoint template, Do you not want to follow the grid and do something custom?   
- Minimum and maximum power option.
- Smooth transitions, minimum and maximum different in setpoint changes.
- Smooth transitions, Smoothing factor above adjustable level.
- Smooth transitions, seperate smoothing factor when passing zero.
- Start condition, Set a start condition before the script is allowed to run
- Stop action, When the start condition is not met do something else instead. 

<img width="1044"  alt="Marstek XOM 2 0" src="https://github.com/user-attachments/assets/0f1e73fd-308e-4ece-9f8b-b71fc2fe4a7a" />

