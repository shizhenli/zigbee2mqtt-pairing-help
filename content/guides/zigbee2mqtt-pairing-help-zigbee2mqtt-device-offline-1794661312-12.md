---
title: "Zigbee2MQTT Device Offline After Restart: Why Entities Vanish and How to Bring Them Back"
description: "All entities become unavailable after a Zigbee2MQTT or broker restart. Learn how to diagnose and restore your device without guesswork."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "All entities become unavailable after a Zigbee2MQTT or broker restart. Learn how to diagnose and restore your device without guesswork."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-17T12:13:06+08:00
publishDate: 2026-11-17T12:13:06+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or your MQTT broker, and now every entity from your new Zigbee device shows as unavailable, leaving you stuck before you can run a proper diagnosis.

## Check the coordinator and network state

Open the Zigbee2MQTT web interface and confirm the coordinator is online. A green status and a recent last seen timestamp mean the USB adapter is working. If the coordinator is offline, stop here and fix the USB connection first. Next, check the device's last seen time in the Devices list. If it is more than a few minutes old, the device has not re-joined after the restart. This is a common reason a **zigbee2mqtt device offline** appears even when the hardware is fine.

## Verify MQTT retention and availability settings

In your configuration, ensure `retain` is enabled for MQTT messages. Without retained messages, the broker restart wipes the device state, and Zigbee2MQTT cannot republish it until the device sends an update. Also check that `availability` is not set to a topic the device never publishes. If it is, disable availability for that device or correct the topic.

## Run a controlled verification test

Restart Zigbee2MQTT only, not the broker. Watch the device's last seen time. If it updates within two minutes, the issue was broker retention. If it stays stale, press the device's pairing button once to wake it, then check again. A fresh timestamp confirms the device is reachable.

## Rollback and recovery

If the device remains unavailable, restore your previous Zigbee2MQTT configuration from a backup and restart. Then re-pair the device if needed. For persistent cases,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration details.
