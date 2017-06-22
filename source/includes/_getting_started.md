
## Getting Started

> Adding a Freewrite USB ethernet device on Linux:

  ```bash
# /etc/network/interfaces
allow-hotplug usb0
auto usb0
iface usb0 inet static
address 192.168.99.44
netmask 255.255.255.0
```

To develop on your Freewrite, you will need:

* A registered Developer account on [Postbox](https://postbox.getfreewrite.com)
* A USB-C cable and your Freewrite device
* A static USB Ethernet connection to your Freewrite
    * *An example is provided at right for Linux developers.*
* An sFTP client like [WinSCP](https://winscp.net/) or [Cyberduck](https://cyberduck.io/)

The following credentials allow sFTP access to the `extensions/` folder on your Freewrite for local extension development:

`sdk:sdk@192.168.99.190`
