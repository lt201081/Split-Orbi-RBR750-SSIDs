# Split-Orbi-RBR750-SSIDs
Split the Orbi RBR750 2.4ghz and 5ghz SSIDs permanently

## Directions

If you want the split SSID to persist on boot, do the following:

1. Grab your two SSIDs:
uci show | grep -i SSID_NAME_HERE
Output: wireless.FhAp2.ssid='SAME_SSID', wireless.FhAp5.ssid='SAME_SSID'

2. FhAp2 is your 2.4ghz SSID string. Write that down.

3. Create a new file with the following name and in this directory: /etc/rc.d/S99whatever_here
The requirement is that the file is named S99, and then whatever else afterward (such as S99Split). S99 indicates "Start" (I believe) and the 99 indicates the order at which it's executed, which we want at the end of boot.

4. vi /etc/rc.d/S99whatever_here
Look up how to edit and save/quit if you are unfamiliar with vi

5. Paste the following bash script:

#!/bin/sh /etc/rc.common

START=99

start() {
	uci set wireless.FhAp2.ssid='DIFFERENT_SSID'
	uci commit wireless
	reload_config
}

6. chmod +x /etc/rc.d/S99whatever_here

7. Reboot for results to take effect

Note: You do not need to do this to the satellites as it will propegate to those systems automatically.
