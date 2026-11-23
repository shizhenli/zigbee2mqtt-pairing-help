---
title: "Zigbee2MQTT Device Unavailable After Restart: Fix the Lost Connection"
description: "Troubleshoot a Zigbee2MQTT device that becomes unavailable after a service restart. Learn to check MQTT, coordinator, and device state, then verify recovery."
seo_title: "Zigbee2MQTT Device Unavailable After Restart: Step-by-Step Fix"
seo_description: "Troubleshoot a Zigbee2MQTT device that becomes unavailable after a service restart. Learn to check MQTT, coordinator, and device state, then verify recovery."
keywords:
  - "zigbee2mqtt device unavailable after restart"
date: 2026-11-23T11:13:37+08:00
publishDate: 2026-11-23T11:13:37+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the broker, and now your new Zigbee device shows as unavailable in Home Assistant or your dashboard.

## Check the coordinator and MQTT connection first

Open the Zigbee2MQTT log and look for a line like `Coordinator firmware version` and `MQTT publish`. If the log shows `MQTT connection failed` or `Coordinator not found`, the restart did not complete cleanly. Stop the service, unplug the USB coordinator for ten seconds, plug it back in, and start Zigbee2MQTT. Wait for the log to show `Zigbee2MQTT started` before testing the device.

## Inspect the device state in the frontend

Go to the Zigbee2MQTT frontend and select the device. If its last seen time is older than the restart time, the device did not rejoin. Press the device's pairing button once (do not hold it) and watch for `Device ... joined` in the log. If the device is battery-powered, replace the battery first; a weak battery often prevents rejoin after a restart.

## Verification test

After the device rejoins, toggle it once from the frontend. Confirm the state changes in the frontend and in your dashboard within five seconds. Then restart Zigbee2MQTT again and check that the device remains available. If it becomes unavailable again, the issue is likely the coordinator's network key or a weak mesh link, not the device.

## Rollback and recovery

If the device worked before the restart, restore your last working `configuration.yaml` and `database.db` backup, then restart. This undoes any accidental coordinator or network key change. If the problem persists, capture the log from startup to the first unavailable message.

For a controlled diagnosis of your specific logs,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).

A single **zigbee2mqtt device unavailable after restart** is usually a rejoin or coordinator timing issue, not a dead device.
