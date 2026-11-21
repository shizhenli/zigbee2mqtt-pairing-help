---
title: "Zigbee2MQTT Device Unavailable After Restart: Fix the Stale State"
description: "All Zigbee2MQTT entities turn unavailable after a service or broker restart? Here's a focused fix for stale retained state and a verification test."
seo_title: "Zigbee2MQTT Device Unavailable After Restart — Fix It"
seo_description: "All Zigbee2MQTT entities turn unavailable after a service or broker restart? Here's a focused fix for stale retained state and a verification test."
keywords:
  - "zigbee2mqtt device unavailable after restart"
date: 2026-11-21T17:06:21+08:00
publishDate: 2026-11-21T17:06:21+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the MQTT broker, and now every entity shows unavailable even though the device worked before the restart.

## Check the retained state first

This usually isn't the device failing; it's stale retained MQTT state being republished before Zigbee2MQTT reconnects to the coordinator. Open your MQTT broker's client (MQTT Explorer or mosquitto_sub) and inspect the retained topics under `zigbee2mqtt/<friendly_name>/availability` and `zigbee2mqtt/bridge/state`.

Interpretation: if `bridge/state` is `offline` while Zigbee2MQTT is running, the service hasn't finished starting. If `bridge/state` is `online` but the device topic still says `offline`, the retained message is stale. If both are correct but Home Assistant still shows unavailable, the discovery topic is the culprit.

## Clear the stale retained message

Stop Zigbee2MQTT. Publish an empty retained payload to the device availability topic to delete it, then start Zigbee2MQTT and let it republish fresh state. Do not delete the whole `zigbee2mqtt` tree; that forces re-interviewing every device.

## Verification test

After restart, wait two minutes, then confirm `bridge/state` is `online` and the device's availability topic reports `online`. Toggle the device once and watch the state topic update. If entities recover, the fix held. If a single device stays offline while others are fine, the problem is that device's route, not the restart.

## Rollback note

If clearing retained messages makes things worse, restore your broker's retained-state backup or re-pair only the affected device. This is why a **zigbee2mqtt device unavailable after restart** issue should be diagnosed before mass-deleting topics.

If the state stays inconsistent,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and topic dump.
