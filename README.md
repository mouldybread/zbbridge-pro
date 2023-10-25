zbbridge-pro
work zbbridge-pro sonoff on esphome

Article website haade
sources
[Github Giancky79](https://github.com/Giancky79/ZB-Bridge-P)

Update firmware
firmware
firmware launchpad

## Install cc2538-bsl
```
mkdir cc2538-bsl
cd cc2538-bsl
curl -sSL https://github.com/JelmerT/cc2538-bsl/archive/refs/heads/master.tar.gz | tar xz --strip 1
```

# Install dépendances
```
pip3 install -r requirements.txt
```

**Lorsque la led verte s'allume lancer le script de mise à jour**

```
sudo python3 cc2538-bsl.py -p socket://ip-gw:6638 -b 460800 -evw ../firmware/CC1352P2_CC2652P_launchpad_coordinator_20230507.hex
```