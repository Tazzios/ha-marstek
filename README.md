
Github to share home assistant automations for the marstek.

XOM stand for X on the meter. as alternative for NOM(staat voor Nul op de Meter)

marstek xom blueprints requirements
- Marstek battery
- Lilygo with ESPHome https://github.com/Superduper1969/MarstekVenus-LilygoRS485
  - Neccesary entities names, (the part before the underscore you can change). 
    -   _rs485_control_mode
    -   _forcible_charge_discharge
    -   _ac_power
    -   _forcible_charge_power
    -   _forcible_discharge_power
    -   _state_of_charge
   
**marstek xom blueprint**  
Based on the work of PimDoos https://github.com/PimDoos/ha-sessy-examples/tree/main  
Features:
- Xom Load/discharge, NOM, XOM only load, XOM only discharge.
- load balancing
- Battery rolation on day

**Marstek x range om Blueprint**
Same as xom with the addition that you can set an range as target. 

For example if your fuse can handle max 2300watt you can set an -2300 till 2300 target. While in this range the battery will do nothing if you go above or below it it will charge/discharge.
