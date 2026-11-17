---
title: "Zigbee2MQTT MQTT Connection Fails: Diagnose Broker Publishing"
description: "Troubleshoot Zigbee2MQTT when MQTT connection fails and entities stay unavailable. Check broker settings, credentials, and network, then verify with a test publish."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT when MQTT connection fails and entities stay unavailable. Check broker settings, credentials, and network, then verify with a test publish."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-17T10:13:07+08:00
publishDate: 2026-11-17T10:13:07+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have Zigbee2MQTT running with a USB coordinator and a new Zigbee device, but at the mqtt connection fails step the logs show it cannot publish to the broker and entities remain unavailable.  

## Check the Broker Address and Port
Open your Zigbee2MQTT configuration and confirm the mqtt server value matches your broker exactly. For a local broker, use localhost or 127.0.0.1 only if Zigbee2MQTT runs on the same host; otherwise use the broker's LAN IP. Verify the port, typically 1883 for plain MQTT or 8883 for TLS. If TLS is enabled, ensure the certificate path and CA are correct. A wrong host, port, or protocol will cause connection refusal or timeout in the log.

## Verify Credentials and Permissions
Check the username and password in the configuration against the broker's user list. A common failure is a typo or an empty password when the broker requires authentication. Confirm the broker allows the user to publish and subscribe to zigbee2mqtt/#. If you use Mosquitto, inspect its log for denied connections; an "not authorised" message points to credentials or ACLs.

## Test the Network Path
From the Zigbee2MQTT host, run a quick TCP check to the broker port, for example using nc -zv <broker-ip> 1883. A successful check returns "succeeded" or "open"; a refused or timed-out result means firewall, Docker networking, or broker binding is blocking the path. If Zigbee2MQTT runs in Docker, avoid localhost for the broker unless using host networking.

## Verification Test
After correcting the setting, restart Zigbee2MQTT and watch the log for a successful MQTT connection line. Then publish a test message to zigbee2mqtt/bridge/state and confirm the broker receives it. Finally, check that your new device's entity updates in your home automation UI.

## Rollback and Recovery
If the change breaks startup, revert to the previous configuration file backup and restart. Keep a copy of the working config before editing. For persistent **zigbee2mqtt mqtt connection** failures after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and broker configuration.
