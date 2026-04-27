Version 2.0  
Breaking: Sort by soc is now a integer instead of boolean      
New: Start condition
New: Adjustabel Sort by soc percentages.
New: Stop action
New: Setpoint template
Fix: Sort by soc was always applied 
Improved: Blueprint inputs, reordered inputs, update text and collapsed sections
Improved: Code, split max difference and absolute limit
Improved: Code, search enitities in one place
  
Version: 1.9  
New: [HA integration marstek venus modbus](https://github.com/ViperRNMC/marstek_venus_modbus/tree/main) support  

Version: 1.8 Let's go smooth!  
Breaking: smoothing is renamed to smoothing_max_watts  
New: minimum different in setpoint change  
New: Smoothing factor above delta x   
New: Smoothing factor when passing zero  

Version: 1.7  
New: Support for [fonske M5stack](https://github.com/fonske/MarstekVenus-M5stackRS485) and [fonske Lilygo](https://github.com/fonske/MarstekVenus-LilygoRS485)  
Fix: variable name in battery ac power calculation #4

Version: 1.6  
Improved: less modbus updates  
fix: Rewrite, keep SOC`s within 10% of each other  
New: Debugging shown in trace

Version: 1.5  
New: Keep SOC`s within 10% of each other

Version: 1.4  
New: Added max power  
Improved: removed unused parameters  
Improved: code variable order

Version: 1.3  
New: Added minimum power  
Fix: max power 2500 instead of 2200  
Improved: changed priority offset default to day of year.  

Version: 1.2  
**Breaking change**: 'Minimum power setpoint' is inverted and renamed to 'Maximum Charge'  
New: Checks the soc during running the script for min and max.  
Improved: Refactored min and max power setpoints, also new renamed.  
Improved: Structured and reordered the settings in sections.   
Improved: set default interval and timeout time.

Version: 1.1  
New:  Target range instead of one setpoint.  

Version: 1.0  
Edited PimDoos: [HA Sessy NOM](https://github.com/PimDoos/ha-sessy-examples/tree/main) to work with Marstek and lilygo modbus [MarstekVenus-LilygoRS485](https://github.com/Superduper1969/MarstekVenus-LilygoRS485).  
Features:
- Rotates battery priority to ensure equal usage over time  
- Dynamic load balancing across multiple batteries  
- SOC-based inclusion/exclusion for optimal battery health  
- Optional offsets for other power consumers (e.g., EV chargers)  
- Smooth transitions between setpoints to prevent sudden battery stress  

