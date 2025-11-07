
Github to share home assistant automations for the marstek.

**marstek xom blueprint**  
Based on the work of PimDoos https://github.com/PimDoos/ha-sessy-examples/tree/main  
Features:
- Xom Load/discharge, NOM, XOM only load, XOM only discharge.
- load balancing
- Battery rolation on day

Requirements
- Marstek battery
- Lilygo with ESPHome https://github.com/Superduper1969/MarstekVenus-LilygoRS485
  - Neccesary entities names, (the part before the underscore you can change). 
    -   _rs485_control_mode
    -   _forcible_charge_discharge
    -   _ac_power
    -   _forcible_charge_power
    -   _forcible_discharge_power
    -   _state_of_charge
