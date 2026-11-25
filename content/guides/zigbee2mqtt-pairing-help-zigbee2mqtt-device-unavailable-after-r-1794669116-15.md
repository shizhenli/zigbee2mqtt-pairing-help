---
title: "Zigbee2MQTT Device Unavailable After Restart: Restore the Expected State"
description: "All entities go unavailable after a Zigbee2MQTT or broker restart. Follow these checks to confirm the device state and restore availability."
seo_title: "Zigbee2MQTT Device Unavailable After Restart: Fix It"
seo_description: "All entities go unavailable after a Zigbee2MQTT or broker restart. Follow these checks to confirm the device state and restore availability."
keywords:
  - "zigbee2mqtt device unavailable after restart"
date: 2026-11-25T12:13:32+08:00
publishDate: 2026-11-25T12:13:32+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the MQTT broker, and now every entity from your new Zigbee device shows as unavailable. Let's confirm what state the device is actually in before changing anything.

## Check the coordinator and network state

Open the Zigbee2MQTT frontend and look at the coordinator status. If it shows offline or the USB path is missing, the restart did not bring the adapter back. Confirm the USB device is still present on the host with `ls /dev/serial/by-id/` and that the configured path matches. If the coordinator is online, open the device in the Devices list and check its last seen time. A last seen older than the restart means the device has not rejoined; a recent last seen means the device is talking but its state is not being published.

## Check MQTT publishing

Inspect the broker logs for the Zigbee2MQTT client. If the client reconnected but the retained availability topic is stale, entities stay unavailable. Subscribe to `zigbee2mqtt/bridge/state` and confirm it reads `online`. Then check the device's availability topic, usually `zigbee2mqtt/<friendly_name>/availability`. A retained `offline` message there explains the symptom.

## Verification test

Power-cycle the Zigbee device once, wait two minutes, and watch its last seen value and availability topic. If both update, the device is back. If only last seen updates, the availability topic is the fault. If neither updates, the device has not rejoined and needs to be re-paired.

## Rollback and recovery

If you changed the coordinator path or network key during troubleshooting, restore the previous configuration and restart. Do not remove the device from the database until you have confirmed the coordinator is online, because removal forces a full re-pair. If the **zigbee2mqtt device unavailable after restart** persists after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration.
