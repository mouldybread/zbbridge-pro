Repository of hack gateway sonoff zbbridge-p pro with esphome for work on Home assistant, with upgrade of zigbee firmware

[tutorial of installation in esphome](https://haade.fr/fr/blog/flasher-zbbridge-pro-esphome-home-assistant)

## many thanks
many thanks to Giancky79 works
[Repository source Github Giancky79](https://github.com/Giancky79/ZB-Bridge-P)

# Upgrade firmware Z-stack Zigbee to Zbbridge-p

## First

- Download this [repository](https://github.com/haade-administrator/zbbridge-pro/archive/refs/heads/main.zip)
- extract folder
- go to zbbridge-pro/ folder
- open terminal

or you can use ```git clone https://github.com/haade-administrator/zbbridge-pro.git```

## Second Install dépendances
```
pip3 install -r requirements.txt
```
- go to cc2538-bsl/ folder
- change address socket://ip-gw:6638 by you're ip
- baudrate 460800 is more IMPORTANT for load this script

```
sudo python3 cc2538-bsl.py -p socket://ip-gw:6638 -b 460800 -evw ../firmware/CC1352P2_CC2652P_launchpad_coordinator_20230507.hex
```