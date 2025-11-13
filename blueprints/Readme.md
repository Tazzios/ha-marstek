

# Marstek X Range OM Blueprint 
This Home Assistant automation controls Marstek batteries according to a **grid sensor**, managing **charging, discharging, and load balancing** across multiple batteries. It ensures that batteries operate efficiently within set limits and adjusts setpoint range dynamically based on grid consumption, battery SOC, and optional offsets.  
Based on the work of PimDoos: [HA Sessy Examples](https://github.com/PimDoos/ha-sessy-examples/tree/main)  

> **XOM** stands for **X on the Meter**, an alternative to NOM (which stands for Nul op de Meter).

## Key Features
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)  
- Smooth transitions between setpoints to prevent sudden battery stress  
- Rotates battery priority to ensure equal usage over time
- Target range instead of one setpoint.  
 **v1.2**
- Check SOC while script is running, (and not only at beginning)
- Beter structure and naming of the settings.

## Requirements
- **Marstek battery**  
- **Lilygo with ESPHome**  
  - Repository: [MarstekVenus-LilygoRS485](https://github.com/Superduper1969/MarstekVenus-LilygoRS485)  
    Your entity names must end in: (the part before the underscore can be customized)
    - `_rs485_control_mode`  
    - `_forcible_charge_discharge`  
    - `_ac_power`  
    - `_forcible_charge_power`  
    - `_forcible_discharge_power`  
    - `_state_of_charge`  

Example:  
- If your fuse can handle a maximum of 2300 W, set a  range from -2300 to 2300.
- you do not want you battery to which between charging and disharging, set range to -100 and 200. 


# Marstek XOM Blueprint
Old version which is no longer maintained
