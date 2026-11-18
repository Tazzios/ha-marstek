# Energieverdeling zonnepanelen en thuisbatterij

Deze Home Assistant-blueprint berekent automatisch de energiestromen binnen een huishouden van zonnepanelen en/of thuisbatterij.

## Functionaliteiten
- Ondersteunt zowel vermogen (W/kW) als energie (Wh/kWh) als invoer.
- Ondersteunt meerdere sensoren per invoertype.
- Zonneproductie en batterij zijn optioneel.
- Automatische conversie van kW naar W.
- Instelbare afronding van uitvoerwaarden.

## Berekening

De blueprint berekent het totale huisverbruik en verdeelt de energiestromen over 7 categorieën:

- Zonnepanelen → Huis, batterij en net.
- Net → Huis en batterij.
- Batterij → Huis en net.

De zonne-energie wordt eerst aan het huisverbruik toegewezen, vervolgens aan het laden van de batterij en ten slotte aan teruglevering aan het net. 

berekent de volgende energiestromen:
  - Zonnepanelen naar huis.
  - Zonnepanelen naar batterij.
  - Zonnepanelen naar elektriciteitsnet.
  - Elektriciteitsnet naar huis.
  - Elektriciteitsnet naar batterij.
  - Batterij naar huis.
  - Batterij naar elektriciteitsnet.

## Limitaties
Bij het zal het niet 100% correct zijn.
Bij input sensors die niet gelijk lopen kun je rare dingen zien.

## Toepassingen

De berekende gegevens kunnen worden gebruikt voor:

- Energievisualisaties en dashboards.
- Berekening van energiekosten en terugleververgoedingen.

Test voorbeeld:
```YAML
{% set solar_production = 0.500 | float(0) %}
{% set grid_power = 0.000 | float(0) %}
{% set battery_charge = 0.00 | float(0) %}
{% set battery_discharge = 0.200 | float(0) %}


{# --- Grid import/export scheiden --- #}
{% set grid_import = max(grid_power, 0) %}
{% set grid_export = max(-grid_power, 0) %}

{# --- Huisverbruik afleiden --- #}
{% set house_consumption = max(
  solar_production + battery_discharge
  + grid_import - battery_charge - grid_export, 0
) %}

{# --- Zon eerst naar huis --- #}
{% set solar_to_home = min(solar_production, house_consumption) %}

{# --- Resterende zonne-energie --- #}
{% set solar_surplus = max(solar_production - solar_to_home, 0) %}

{# --- Zon naar batterij --- #}
{% set solar_to_battery = min(battery_charge, solar_surplus) %}

{# --- Zon naar grid --- #}
{% set solar_to_grid = max(solar_surplus - solar_to_battery, 0) %}

{# --- Batterij naar grid --- #}
{% set battery_to_grid = min(battery_discharge, grid_export) %}

{# --- Batterij naar huis --- #}
{% set battery_to_home = min(
  max(battery_discharge - battery_to_grid, 0),
  max(house_consumption - solar_to_home, 0)
) %}

{# --- Grid naar batterij --- #}
{% set grid_to_battery = max(battery_charge - solar_to_battery, 0) %}

{# --- Grid naar huis --- #}
{% set grid_to_home = max(
  house_consumption - solar_to_home - battery_to_home, 0
) %}

{# --- RESULTATEN --- #}
Zon → huis: {{ solar_to_home | round(3) }}
Zon → grid: {{ solar_to_grid | round(3) }}
Zon → batterij: {{ solar_to_battery | round(3) }}
Grid → huis: {{ grid_to_home | round(3) }}
Grid → batterij: {{ grid_to_battery | round(3) }}
Batterij → huis: {{ battery_to_home | round(3) }}
Batterij → grid: {{ battery_to_grid | round(3) }}
```

