#ESPHome for the Sonoff ZBBridge Pro

This fork disables the ble-tracker, removed firware related stuff, and switched to esp-idf.

Disabling bluetooth and antenna sharing seems to improve esp32 response times.

The radio firmware needs to be modified for this device to work with ESPHome. This can be achieved by flashing the Sonoff software for this device. Follow their instructions to do so.

See the original version of this software for alternative ways to flash the radio.

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
      esphome/bluetooth.yaml,
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
