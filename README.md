# clean-shutdown

clean-shutdown is a simple daemon that monitors a user-specified GPIO pin and triggers a clean software shutdown when that pin is asserted low.

To install, run `setup.sh`, then create edit `/etc/cleanshutd.conf` as desired.

Note: the default trigger pin is BCM4, which means that if you are using the Zero Lipo there is nothing to do besides running the installer.
