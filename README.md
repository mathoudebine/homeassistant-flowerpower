# homeassistant-flowerpower
Home Assistant Custom component for Parrot FlowerPower

This is offered AS IS. I'm not going to continue updating this. Feel free to fork. 
Thanks to https://github.com/gkreitz/homeassistant-airthings for copy&paste-inspiration! 

FlowerPower has very limited BLE technical documentantion, but for version 1. I have version 2.0.3 so this mainly works with that version. Different versions have different attibutes so your version might not work with this. This version did not give any moisture %, and I think that's because my device is already broken. I release this code, so other's don't have to rewrite it. 

## Dependencies

Bluepy - will be installed automatically by HA core

## Installation

1. Find out the MAC address of your FlowerPower with `hcitool lescan`.
1. Put `__init__.py`, `sensor.py`, `manifest.json` into `<config>/custom_components/parrot_flowerpower/` on your home assistant installation (where `<config>` is the directory where your config file resides).
1. Add the following to your `configuration.yaml` (or modify your `sensor` heading, if you already have one):
```yaml
sensor:
  - platform: parrot_flowerpower
    mac: 00:11:22:AA:BB:CC # replace with MAC of your FlowerPower
    name: Green  # Shall be unique as it is used in entities IDs
```
Then restart Home Assistant and if everything works, you'll have some new sensors.

To add a [Plant monitor](https://www.home-assistant.io/integrations/plant/) from your FlowerPower sensor :

```yaml
# Create plants entities from sensors of FlowerPower
plant:
  name_of_your_plant:
    sensors:
      moisture: sensor.flowerpower_{sensor name}_calibrated_soil_moisture
      battery: sensor.flowerpower_{sensor name}_battery_level
      temperature: sensor.flowerpower_{sensor name}_calibrated_air_temperature
      conductivity: sensor.flowerpower_{sensor name}_soil_ec
      brightness: sensor.flowerpower_{sensor name}_light_intensity
```

After a restart, you can then add a [Plant status card](https://www.home-assistant.io/lovelace/plant-status/) to your dashboard

## Debug

To add debug logs of the component, add the following to your `configuration.yaml`:
```yaml
logger:
  default: warning
  logs:
    custom_components.homeassistant-flowerpower.sensor: debug
```
