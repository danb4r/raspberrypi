# Ubuntu 64-bits on Raspberry Pi 4, fan, shutdown, power-on, etc

## Intro

Ubuntu is a much more stable and mature 64-bit distro to use Pi 4 as a small server. So here is how you can fast setup the cooling fan and add a shutdown and poweron button.

By the time of writting, I was working with Ubuntu 22.04.2 LTS (jammy) in a Raspberry Pi 4 Model B 2019 Quad Core 64 Bit WiFi Bluetooth (4GB).

## Fast track: setting up the fan controller and a shutdown button

```
sudo vi /boot/firmware/config.txt
```

Comment the line bellow to disable I2C. If you need I2C, read on and change the default fan pin to another one not used by I2C.

```
#dtparam=i2c_arm=on
```

Add this lines at the end of the file:

```
# Custom config
dtoverlay=gpio-shutdown,gpio_pin=3
dtoverlay=gpio-fan,gpiopin=12
```

Done. GPIO PIN 3 is now your shutdown and power on pin. Wire it to any GND pin and you Pi will shutdown in on and power on if off. A button may be handful.

See the [Pi's GPIO layout](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#gpio-and-the-40-pin-header) for reference.

## Firmware Config

The `/boot/firmware/config.txt` file we just edited is like a BIOS config for the Pi and Ubuntu fully supports it. [This Pi's documentation](https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt) has all the details about it and what you can do with it.

## Overlays

To know all overlays available to you, just take a look at this file in you system:

```
less /boot/firmware/overlays/README
```

To know more about Pi's Overlays, [here is the docs](https://www.raspberrypi.com/documentation/computers/configuration.html#device-trees-overlays-and-parameters).

## More tips

You can find more tips on how to change your Pi's Ubuntu 64 config in this [Stephane Chauveau's GIST](https://gist.github.com/schauveau/a55eb2811fe12e8ad186d35feb788743), that was my starting point.
