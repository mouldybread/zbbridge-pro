# zbbridge-pro
work zbbridge-pro sonoff on esphome

# Article website haade

# sources

[Github Giancky79](https://github.com/Giancky79/ZB-Bridge-P)

# Update firmware
{% highlight yaml %}
pip3 install -r requirements.txt
{% endhighlight %}

# firmware
[firmware launchpad](https://github.com/Koenkk/Z-Stack-firmware/blob/master/coordinator/Z-Stack_3.x.0/bin/CC1352P2_CC2652P_launchpad_coordinator_20230507.zip)

**Lorsque la led verte s'allume lancer le script de mise à jour**

{% highlight yaml %}
cc2538-bsl -p socket://zbbridge.local:6638 -evw ../firmware/CC1352P2_CC2652P_launchpad_coordinator_20230507.hex