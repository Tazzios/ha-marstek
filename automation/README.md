# ⚡ Marstek Controller

## Overview
This automation acts as a central controller based on electricity prices and battery state of charge (SOC). 
It switches between **charging**, **discharging**, and **netsafe** by enabling or disabling other automations as needed.

## Triggers
- `binary_sensor.my_cheapest_hours`: detects the start/end of cheap hours  
- `binary_sensor.expensive_hours`: detects the start/end of expensive hours  
- `sensor.lilygo_rs485_marstek_battery_state_of_charge`: triggers when battery SOC drops below 15%

## Actions Summary
1. **Turn off all automations** labeled `marstek` to prevent conflicts.  
2. **Conditional logic**:
   - **Expensive hours start** → enable `automation.marstek_xom_ontladen` (discharge)
   - **Cheap hours start** (price difference > €0.10) → enable `automation.marstek_xom laden` (charge)
   - **Battery < 15%** → enable charging until SOC > 20%,
   - **Default** → enable netsafe  discharge `automation.marstek_netsafe`

## Notes
- Price difference check prevents charging when not cost-effective.  
- Price triggers created by : https://github.com/kotope/aio_energy_management
- In my case the netsafe uses the x range blueprint to stay between -2300 and 2300. the other the normal one.

