# bash-libnetwork

A Bash library with basic networking utilities

Install
-------

You can clone this repository or download it as a zip file. To clone:

    $ git clone https://github.com/david-moreno/bash-libnetwork.git
    $ cd bash-libnetwork
    $ sudo make install

Uninstall
---------

Using the cloned/unzipped directory:

    $ cd bash-libnetwork
    $ sudo make uninstall

Usage
-----

#### net_available_ifaces
Returns the available network interfaces

#### net_iface_isavailable *iface*
Checks if *iface* exists

#### net_get_iface_ip *iface*
Returns the IP address of *iface*

#### net_get_iface_mac *iface*
Returns the MAC address of *iface*

#### net_get_iface_mtu *iface*
Returns the MTU value of *iface*

#### net_iface_up *iface*
Checks if *iface* is UP

#### net_get_iface
Returns the current active network interface

#### net_get_gateway
Returns the current gateway IP address

#### net_connected_inet
Checks if the host is connected to internet

#### net_iface_iswireless *iface*
Checks if *iface* is a wireless device

Example
-------

```bash
#!/bin/bash

#Includes the library into the script
source "/usr/lib/bash/libnetwork"

echo "Available network interfaces:"
for i in `net_available_ifaces`; do
	echo "- $i"
done

if (( ! `net_connected_inet` )); then
	echo "No Internet connection"
	exit
fi

iface=`net_get_iface`
if [ -z "$iface" ]; then
	echo "No active network interfaces founded"
	exit
fi

echo -e "\nThe current active network interface is: $iface"
if (( `net_iface_iswireless $iface` )); then
	echo -e "\t$iface is wireless"
fi
echo -e "\tIP: " `net_get_iface_ip $iface`
echo -e "\tMAC: " `net_get_iface_mac $iface`
echo -e "\tMTU: " `net_get_iface_mtu $iface`

echo -e "\nGateway: " `net_get_gateway`
```
