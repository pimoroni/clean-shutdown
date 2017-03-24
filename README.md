# clean-shutdown

`clean-shutdown` is a simple daemon that monitors a user-specified GPIO pin and triggers a clean software shutdown when that pin is asserted low. It offers a way to customise the behaviour of the monitoring as well as shutdowm to fit numerous use-cases.

## Installation

To install, run `setup.sh` and when prompted enter the pin you would you like to use as trigger for the shutdown.

The setup script expects an integer value between 4 and 27 (you can use others outside this range by manually editing the config file as explained below, but there are caveats so if it does not quite work, you're on your own!)

If you are unsure how to clone this repository, you can also use the following command to make your life easier:

```
curl https://get.pimoroni.com/cleanshutdown | bash
```

If you are using a [Zero LiPo](https://shop.pimoroni.com/products/zero-lipo), we have a dedicated script that will ensure the daemon configuration is optimal for that scenario:

```
curl https://get.pimoroni.com/zerlipo | bash
```
(you won't be prompted for a pin, BCM4 will be used automatically)

## Usage

There is really not a lot that needs to be done once the daemon is in place - which will be the case after installation and reboot... this is all vey straightforward!

That said, `clean-shutdown` has some interesting features that your particular use-case may require. For example, if you are using an input trigger you would normally expect the shutdown to occur as soon as you press the control. But what if that is not what you want?

`clean-shutdown` provides several useful features to adapt the shutdown behaviour or exact monitoring environment to your project requirements, without requiring you to mess with the daemon code, or understand what it does in the smaller details.

If you find yourself in such a need, fire up your favourite editor and open `/etc/cleanshutd.conf`. The parameters documented below can be customised as desired.

Note that in order for parameter changes to take effect the deamon has to be restarted. The easier way to do that is to reboot the Pi, or run:

```
sudo service cleanshutd restart
```

## Parameters

### `daemon_active`

This is a pretty hacky way to passify the daemon without needing to delve into the details of [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Set to `0` to deactivate the daemon (technically the daemon will be started at boot time but it will do absolutely nothing). Set to `1` to reactivate.

### `shutdown_delay`

Most of the time you probably want your Pi to shutdow as soon as the trigger occurred, but sometimmes, like with the Zero Lipo, once the battery warning has been detected you still got some life of the LiPo before it is necessary to shut it down (the warning is activated at 3.4V, but a protection circuit will completely cut off the supply at 3.0V). The unit here is expressed in minutes (`0`, the default means immediate shutdown).

### `polling_rate`

This parameter determines how often the trigger is checked for. Normally a small, but reasonable value, like a second or 2 is adequate to detect a button press, but if you take the Zero Lipo example it really does not matter if the monitoring is more laxed, say every 30 seconds or so. There may be other use-cases where smaller or larger values are optimal, so there's a parameter you can if you finfd yourself in one. Units are in seconds here.

### `trigger_pin`

Normally you'll set this up at install timme and won't need to change it, but... as we do, next week you might buy a nice shiny (Pimoroni) HAT or pHAT and find that the pin you had your clean shutdown trigger wired to is required by your new friend. Just move the trigger button to anoter pin and reboot! The unit used for this parameter is the bcm number of the pin (4 or above recommended, 0-3 have particularities that make them slightly less straightforward to use, though the daemon will happily monitor them, as long as you know what you're doing it's OK to use them).
