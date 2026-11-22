---
title: "Zigbee2MQTT Device Offline After Restart: Why Entities Vanish and How to Restore Them"
description: "After restarting Zigbee2MQTT or your broker, all entities show unavailable. Follow these checks to diagnose and restore your device without guesswork."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "After restarting Zigbee2MQTT or your broker, all entities show unavailable. Follow these checks to diagnose and restore your device without guesswork."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-22T12:14:01+08:00
publishDate: 2026-11-22T12:14:01+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the MQTT broker, and now every entity from your new Zigbee device shows as unavailable.

## Check the coordinator and network state
Open the Zigbee2MQTT web interface and confirm the coordinator is online. Look at the device list: if the device shows a last-seen timestamp older than the restart, it has not re-joined. A green coordinator status with a grey device icon means the radio is fine but the device is not communicating.

## Verify MQTT topics and retained messages
Use an MQTT client to subscribe to `zigbee2mqtt/bridge/state`. If it shows `offline`, Zigbee2MQTT has not fully connected to the broker. Also subscribe to `zigbee2mqtt/<device_name>/availability`; a retained `offline` payload after restart indicates the device's availability topic was not refreshed. If these topics are missing, the device may not be paired correctly.

## Inspect the device's availability settings
In the device's settings, check that `availability` is enabled and the topic matches. A common cause of a **zigbee2mqtt device offline** after restart is a retained availability message that never updates because the device is asleep or out of range. Wake the device manually (press its pairing button once) and watch the last-seen time update.

## Verification test
Restart Zigbee2MQTT again. Immediately watch the device's last-seen timestamp and the availability topic. If the timestamp updates within two minutes and the availability payload changes to `online`, the issue is resolved. If not, proceed to recovery.

## Rollback and recovery
If the device remains unavailable, remove it from Zigbee2MQTT (force remove if needed), reset the device, and pair it again. Before doing so, note its current settings. After re-pairing, verify the availability topic updates correctly. If the problem persists across multiple devices, the coordinator or broker configuration may be at fault. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
