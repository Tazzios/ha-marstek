# X Range on the Meter - Documentation
This documentation is (about) the same for Sessy and Marstek.

## Index
- [Getting Started](#getting-started)
- [Inputs overview](#inputs-overview)
- [Key Concepts](#key-concepts)

# Getting Started

To successfully configure the blueprint, you need to fill in atleast the following fields:

- **Battery's**: Select the batteries you want to use.
- **Grid**: measuring grid net consumption.
- **Grid target minimum value**: Set the minimum value the system should aim for.
- **Grid target maximum value**: Set the maximum value the system should aim for.
 
# Inputs overview
Complete reference guide for all configuration inputs in the battery control blueprint.


## Battery Selection Section

| Field | Explanation | Example |
|-------|-------------|---------|
| **Batteries** | Select one or more Battery devices to control. | Select "Marstek Venus Modbus" and "Marstek m1" |
| **Minimum State of Charge** | Batteries below this level won't participate during discharge. Prevents over-discharging. Range: 0-50% | Set to 20 to prevent discharging below 20% SoC |
| **Maximum State of Charge** | Batteries above this level won't participate during charge. Prevents over-charging. Range: 50-100% | Set to 90 to stop charging when batteries reach 90% SoC |


## Battery Rotation Section

| Field | Explanation | Example |
|-------|-------------|---------|
| **Order by State of Charge** | When enabled (default: true), orders batteries by State of Charge so they stay within 10% of each other. Overrides priority offset template for balanced aging. | Enable (true) for automatic SoC balancing; disable (false) for fixed priority order |
| **Priority offset template** | Template to rotate battery priority based on a calculated value. Only used if "Keep SOCs within 10%" is disabled. | `{{ now().timetuple().tm_yday }}` rotates daily or `{{ now().hour }}` rotates hourly (not recommended) |



## Power Section

| Field | Explanation | Example |
|-------|-------------|---------|
| **Battery Minimum power** | Minimum power (W) required to activate a single battery for charge or discharge. Prevents inefficient small power operations. Range: 0-2500W | Set to 50 to avoid activating batteries for loads under 50W |
| **Max optimal power** | Power threshold (W) before distributing load across multiple batteries. Below this uses one battery; above this distributes load. Range: 50-2500W | With 2000W: 1500W uses 1 battery; 2500W uses 2 batteries |
| **Battery maximum power** | Maximum power (W) a single battery can output for charge or discharge. Protects battery from overcurrent. Range: 50-2500W | Set to 3000 for high-capacity; 2000 for smaller batteries |
| **Maximum charging** | Maximum total charging power (W) across all batteries combined. Set to 0 to disable charging entirely. Range: 0-12000W | Set to 8000 to limit total charging to 8kW max |
| **Maximum discharging** | Maximum total discharging power (W) across all batteries combined. Set to 0 to disable discharging entirely. Range: 0-12000W | Set to 10000 to limit total discharging to 10kW max |

## Setpoint Section
A **setpoint** is the target power value (in Watts) that the blueprint calculates to control your batteries. It tells the batteries how much power they should charge or discharge to maintain your desired grid operating point.

| Field | Explanation | Example |
|-------|-------------|---------|
| **Grid** | Select the grid power sensor measuring net consumption. Must be a power sensor with kW or W unit. Positive = grid import, negative = grid export. | Select `sensor.grid_power` or `sensor.net_consumption` |
| **Grid target minimum value** | Lower limit of grid target band (W). When grid import falls below this, batteries discharge to return to band. Range: -10000 to 5000W | Set to -500 creates deadband where grid can export 0-500W without triggering charge |
| **Grid target maximum value** | Upper limit of grid target band (W). When grid import exceeds this, batteries charge to return to band. Range: -5000 to 10000W | Set to 500 creates deadband where grid can import 0-500W without triggering discharge |

## Advanced setpoint settings
Options to adjust or override the setpoint.

| Field | Explanation | Example |
|-------|-------------|---------|
| **Offset entities** | Optional sensors whose values (in Watts) are subtracted from grid reading. Excludes certain loads from affecting battery control. Default: none (empty list) | Select `sensor.car_charger_power` and `sensor.pool_heater` to exclude them |
| **setpoint template** | Advanced: Custom Jinja2 template to modify target setpoint. Available variable: `corrected_net_load`. Use to apply custom logic. Default: `{{ corrected_net_load }}` | `{{ (corrected_net_load * 0.8) \| int }}` reduces setpoint to 80%; `{{ corrected_net_load + 500 }}` adds 500W offset.  `{{ corrected_net_load + states.sensor.sessy_deem_power.state \| int }}` Distract the power from a other brand battery(watch the + as the value is seen from the battery instead of the grid). `{{ states.sensor.solar_power.state \| int }}` Set it the same to your solar. |

## Smoothing Section

| Field | Explanation | Example |
|-------|-------------|---------|
| **Minimum differents** | Hysteresis value (W) - minimum change between old and new setpoint to trigger action. Prevents frequent switching due to noise. Range: 0-500W | Set to 50 to ignore changes smaller than 50W |
| **Maximum differents** | Maximum allowed change (W) between old and new setpoint per cycle. Limits ramp rate to avoid spikes . Range: 50-10000W | Set to 1000 to limit power changes to 1kW per update cycle |
| **Smoothing above** | Applies exponential smoothing only when above this threshold (W). Below this threshold full setpoint is used. Range: 0-5000W | With 1000W: changes under 1000W apply instantly; above 1000W apply smoothing factor |
| **Smoothing factor** | Damping factor for exponential smoothing (0.01-1). Lower = slower response, more stable; higher = faster response. 1 = no smoothing. Default: 0.7 | `0.5` = change is 50% toward target per cycle; `0.9` = very gradual 9-step response |
| **smoothing factor when passing zero** | Special damping factor when crossing zero (switching between charge/discharge). Lower prevents rapid oscillation. Range: 0.01-1. Default: 0.3 | `0.2` = cautious 5-step crossing; prevents flipping between modes |

## Script Section

| Field | Explanation | Example |
|-------|-------------|---------|
| **Start condition** | Optional conditions that must be true to activate automation. Allows time-based or mode-based control. Default: none (always active) | Only run if `input_boolean.battery_enabled = on` or during `time: before: "22:00"`. Make a dropdown helper to choose which blueprint has to run. `input_select.Marstek_control.state = "NOM"` |
| **Stop action** | Action when start condition is not met. Options: "Run script with setpoint 0" or "Do not run the script". When you use the "do not run" option understand that the battery will continue what is was doing. Default: "Run script with setpoint 0" | Select "Do not run the script" to completely pause during night hours |
| **Additional stop actions** | Custom action(s) when start condition is not met. | Stop the battery if you selected the "Do not run the script" at stop action. notification, add extra delay, Stop the automation it self, start another |
| **Update interval** | Minimum time to wait between accepting new grid data updates. Default: 10 seconds | Set to 5 seconds for fast-responding systems; 30 seconds for stable/slow systems |
| **Debug** | Enable debug logging to Home Assistant trace/logbook. Shows all variables during execution for troubleshooting. Default: false | Enable to see setpoint calculations, battery activation, and offsets |

# Key Concepts

## Load Balancing Example
With `Max optimal power` = 2000W, `Battery maximum power` = 2500W and 3 batteries:
- 1500W load → uses 1 battery at 1500W
- 4000W load → distributes across 2 batteries (2000W each)
- 6600W load → distributes across 3 batteries (2200W each)

## SoC Sorting Example
With `Order by State of Charge` on 10% and `setpoint < 0` (charging):
- Battery A: 80% SoC (rounded to 80%)
- Battery B: 42% SoC (rounded to 40%)
- Battery C: 68% SoC (rounded to 70%)
- Charging order: B → C → A (lowest to highest, ensures balanced aging)

## Grid target Example
**Grid zero**, min 0 and max 0.  
**Charge only**, min 0 and max 5000. solar charging  
**Discharge only**, min -5000 and max 0.  
**Full charge**, min 5000 and max 5000.  
**Full discharge**, min -5000 and max -5000.  

Depending on your amount of battery`s and grid use you maybe need an higher value then 5000.
Other ways to control this is by adjusting min/Max charging to zero under Power or to create an own setpoint with 'setpoint template'.

## Deadband Example
With `Target minimum value` = -200W and `Target maximum value` = 200W:
- Grid exports 0-200W → no action (within band)
- Grid exports 250W → batteries discharge to return to band
- Grid imports 0-200W → no action (within band)
- Grid imports 250W → batteries charge to return to band

### Smoothing Formula
When crossing zero with `smoothing factor when passing zero` = 0.3:
new_setpoint = (0.3 × raw_setpoint) + (0.7 × battery_current_power)

**Example:**
- Current battery power: -1000W (charging)
- Raw setpoint: +500W (discharge)
- Calculation: (0.3 × 500) + (0.7 × -1000) = 150 - 700 = -550W
- Result: Gradual transition from -1000W to +500W instead of immediate switch


---
