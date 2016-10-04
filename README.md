# WWAN
## Problem
My E7270 came with a DW5811e WWAN-module. However, it seems Debian Stretch was not able to recognize it directly.
`mmcli -L` did not show any modems.

I did find `/dev/cdc-wdm0` and a mention about it in `dmesg` however, as well as the error message:
```
ModemManager[2443]: proxy configuration failed: closed
ModemManager[2443]: <info>  Creating modem with plugin 'Dell' and '2' ports
ModemManager[2443]: <warn>  Could not grab port (usbmisc/cdc-wdm0): 'Cannot add port 'usbmisc/cdc-wdm0', unsupported'
ModemManager[2443]: <warn>  Couldn't create modem for device at '/sys/devices/pci0000:00/0000:00:14.0/usb2/2-5': Failed to find primary AT port
```

## Solution
After a bit of searching, I found [this repo](https://github.com/daniviga/latitude5450) where the owner has a 5809e WWAN-module.
Grabbing his rules.d-script and modifying it with my vendor and device id made NetworkManager find my card after a reboot, and now I'm able to connect.

Put [this file](99-dell5811e.rules) in `/etc/udev/rules.d/` and it should work after a reboot.

## Speeds
83 Mbps down, 46 Mbps up, 18 ms latency
