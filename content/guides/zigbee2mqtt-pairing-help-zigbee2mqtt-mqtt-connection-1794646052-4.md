---
title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
description: "Fix Zigbee2MQTT MQTT connection failures when the broker won't accept publishes. Step-by-step checks for broker address, credentials, and logs."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Troubleshoot Broker Publishing"
seo_description: "Fix Zigbee2MQTT MQTT connection failures when the broker won't accept publishes. Step-by-step checks for broker address, credentials, and logs."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-14T20:04:28+08:00
publishDate: 2026-11-14T20:04:28+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've paired a new Zigbee device, but Zigbee2MQTT can't publish to your broker and entities stay unavailable—stuck at the mqtt connection fails step.

## Check the broker address and port
Open your Zigbee2MQTT configuration and verify the mqtt server field. It should be the broker's IP or hostname and port, for example tcp://192.168.1.50:1883. If it uses localhost, change it to the broker's LAN address unless both run on the same host. A wrong port or protocol will cause an immediate connection refusal.

## Confirm credentials and client ID
Check that the username and password match the broker's user database exactly. If your broker requires a client ID, ensure it is unique. A rejected login usually appears in the Zigbee2MQTT log as 'Connection refused: Not authorized'. Correct the credentials, then restart Zigbee2MQTT.

## Inspect the log for the exact error
Tail the Zigbee2MQTT log and look for the first MQTT error after startup. 'ECONNREFUSED' means nothing is listening at that address; 'Not authorized' means bad credentials; 'Timeout' suggests a firewall or network path issue. Fix the specific error before retrying.

## Verification test
From the Zigbee2MQTT host, run a quick publish test to the broker, for example using mosquitto_pub to the base topic. If that succeeds but Zigbee2MQTT still fails, the problem is in its config. Then restart Zigbee2MQTT and watch for 'Connected to MQTT server'. Confirm entities update in your dashboard.

## Rollback and recovery
If changes make things worse, restore your previous configuration.yaml from backup and restart. This returns you to the last known state so you can retry one change at a time. For persistent **zigbee2mqtt mqtt connection** failures,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and config.
