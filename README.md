# ESPHome for the Sonoff ZBBridge Pro

This fork removes bluetooth and the ble tracker, removes firware related files and switches to esp-idf.

Disabling bluetooth and antenna sharing seems to improve esp32 response times.

The radio firmware needs to be modified for this device to work with ESPHome. This can be achieved by flashing the [Tasmota software](https://zigbee.blakadder.com/Sonoff_ZBBridge-P.html) for this device. Details below.

See the original version of this configuration for alternative ways to flash the radio.

### Is your device alive but the radio not responding to clients? Reflashing might help. See the section below.

## Essentials:
```
external_components:
  - source: github://oxan/esphome-stream-server
```

```
esp32:
  framework:
    type: esp-idf
```
```

packages:
  remote-packages:
    url: https://github.com/mouldybread/zbbridge-pro.git
    ref: main
    refresh: 0s
    files: [
      esphome/esphome.yaml,
      esphome/binary_sensor.yaml,
      esphome/light.yaml,
      esphome/output.yaml,
      esphome/rtttl.yaml,
      esphome/sensor.yaml,
      esphome/switch.yaml,
      esphome/text_sensor.yaml,
      esphome/uart.yaml,
      esphome/stream_server.yaml,
   ]
```
## Flashing:
The sands of time have done a number on this and no one place has all the answers. Even the official docs link to outdated guides. The Sonoff Zigbee Bridge Pro is very well supported by Tasmota. I still prefer ESPHome so I did the following to flash the radio before I installed esphome:

* Install [tasmota32-zbbrdgpro.factory.bin](https://ota.tasmota.com/tasmota32/release/tasmota32-zbbrdgpro.factory.bin) using [Install Tasmota](https://tasmota.github.io/install/)
> [!NOTE]
> It must be the factory image, even if you already have ESPHome on the device. It will "work" if you install an OTA image but you will be missing the file manager.
* Download the latest radio firmware from [here](https://github.com/arendst/Tasmota/tree/development/tasmota/berry/zigbee) - the guides still reference outdated firmware. Tasmota ships with outdated firmware. Press the download button, do not save the file.
* Download [cc2652_flasher.be](https://github.com/arendst/Tasmota/blob/development/tasmota/berry/zigbee/cc2652_flasher.be) [intelhex.be](https://github.com/arendst/Tasmota/blob/development/tasmota/berry/zigbee/intelhex.be) [sonoff_zb_pro_flasher.be](https://github.com/arendst/Tasmota/blob/development/tasmota/berry/zigbee/sonoff_zb_pro_flasher.be)
* Go to Tasmota Device -> Tools -> Manage File System
* Delete the existing files of the same or similar name
* Replace them with the new versions that you downloaded
* REBOOT THE DEVICE
* Go to Tasmota Device -> Tools -> Berry Console
* Utter the following incanation:
  ```
  import sonoff_zb_pro_flasher as cc
  cc.load("SonoffZBPro_coord_20240710.hex")
  cc.check()
  ```
* After some time the output will confusingly appear on the other console. If it reports OK then you can cast the spell:
  ```
  cc.flash()
  ```
* Magic happens. Do not touch the device for 5 minutes, then reboot.

You can now install the ESP Home binary that you've compiled from this repo.
## Repo Structure
As you may have noticed the author of this configuration nested it into many separate includes and I have chosen to keep that structure and the remote includes. You can of course just copy and paste it all into your devices configuration.
## Full configuration
Here is my full working configuration
```
external_components:
  - source: github://oxan/esphome-stream-server

substitutions:
  devicename: zbbridge
  friendly_name: ZB-BRIDGE

esphome:
  name: $devicename
  friendly_name: $friendly_name

esp32:
  framework:
    type: esp-idf       

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "REPLACEME"

ota:
  - platform: esphome
    password: "esphome123"
web_server:
wifi:
  power_save_mode: NONE
  manual_ip:
    static_ip: REPLACEME
    gateway: REPLACEME
    subnet: 255.255.255.0
    dns1: REPLACEME
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Zb-Bridge Fallback Hotspot"
    password: "xBZYfhKalZfW"

captive_portal:


packages:
  remote-packages:
    url: https://github.com/mouldybread/zbbridge-pro.git
    ref: main
    refresh: 0s
    files: [
      esphome/esphome.yaml,
      esphome/binary_sensor.yaml,
      esphome/light.yaml,
      esphome/output.yaml,
      esphome/rtttl.yaml,
      esphome/sensor.yaml,
      esphome/switch.yaml,
      esphome/text_sensor.yaml,
      esphome/uart.yaml,
      esphome/stream_server.yaml,
   ]
```
## GPIO Configuration

 + 2 = blue led
 +  4 = buzzer
 +  13
 +  14
 +  15 = zRST
 +  23 = rx zigbee
 +  21 = green led
 +  22 = boot
 +  19 = tx zigbee
 +  25 = scl
 +  26 = sda
 +  27 = button key
 +  33

# References
https://www.zigbee2mqtt.io/advanced/remote-adapter/connect_to_a_remote_sonoff_zbbridge.html

https://github.com/arendst/Tasmota/discussions/18515

https://digiblur.com/2020/07/25/how-to-use-the-sonoff-zigbee-bridge-with-home-assistant-tasmota/

https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/

https://github.com/arendst/Tasmota/issues/22765

https://zigbee.blakadder.com/Sonoff_ZBBridge-P.html

https://github.com/haade-administrator/zbbridge-pro

