# Marstek XOM Blueprint
This Home Assistant automation controls Marstek batteries according to a **grid sensor**, managing **charging, discharging, and load balancing** across multiple batteries. It ensures that batteries operate efficiently within set limits and adjusts setpoints dynamically based on grid consumption, battery SOC, and optional offsets.  
Based on the work of PimDoos: [HA Sessy Examples](https://github.com/PimDoos/ha-sessy-examples/tree/main)  

> **XOM** stands for **X on the Meter**, an alternative to NOM (which stands for Nul op de Meter).

## Key Features
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)  
- Smooth transitions between setpoints to prevent sudden battery stress  
- Rotates battery priority to ensure equal usage over time  

## Marstek XOM Blueprint Requirements
- **Marstek battery**  
- **Lilygo with ESPHome**  
  - Repository: [MarstekVenus-LilygoRS485](https://github.com/Superduper1969/MarstekVenus-LilygoRS485)  
  - Necessary entity naming convention (the part before the underscore can be customized):
    - `_rs485_control_mode`  
    - `_forcible_charge_discharge`  
    - `_ac_power`  
    - `_forcible_charge_power`  
    - `_forcible_discharge_power`  
    - `_state_of_charge`  

# Marstek X Range OM Blueprint
Same to the XOM blueprint, but allows setting a **target range**.  

Example:  
- If your fuse can handle a maximum of 2300 W, you can set a target range from `-2300` to `2300`.  
- While the load is within this range, the battery does nothing.  
- If the load goes above or below the range, the battery will charge or discharge accordingly.  
