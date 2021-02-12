#!/bin/sh /etc/rc.common

START=99

start() {
	uci set wireless.FhAp2.ssid='DIFFERENT_SSID'
	uci commit wireless
	reload_config
}
