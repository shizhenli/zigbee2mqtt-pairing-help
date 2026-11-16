---
title: "Zigbee2MQTT Device Unavailable After Restart: Fix a Stale Pairing"
description: "A new Zigbee device goes unavailable after every Zigbee2MQTT or broker restart. Diagnose stale pairing state, verify with a controlled restart, and recover safely."
seo_title: "Zigbee2MQTT Device Unavailable After Restart — Fix Stale Pairing"
seo_description: "A new Zigbee device goes unavailable after every Zigbee2MQTT or broker restart. Diagnose stale pairing state, verify with a controlled restart, and recover safely."
keywords:
  - "zigbee2mqtt device unavailable after restart"
date: 2026-11-16T10:13:03+08:00
publishDate: 2026-11-16T10:13:03+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You paired a new Zigbee device, then restarted Zigbee2MQTT or the broker, and now every entity shows unavailable.

## Confirm the restart is the trigger

Open the Zigbee2MQTT log and find the restart line. Look for the device's IEEE address appearing after startup. If it is absent, the device was never written to the coordinator's database, so the restart simply exposed a stale pairing. If it appears but no state messages follow, the interview did not complete.

## Check the pairing state

In the frontend, open the device and read its interview status. A completed interview means the database entry exists; an incomplete or missing interview means the pairing was interrupted. Also check that the coordinator's permit join was off before the restart, so no half-finished join was left open.

## Run the verification test

Remove and re-pair the device while watching the log until the interview completes and a state report arrives. Then restart Zigbee2MQTT once, deliberately. If the entity returns available within a minute, the pairing is now persistent. If it still drops, the coordinator database is not being saved on shutdown.

## Recover if it fails again

Stop Zigbee2MQTT, back up the coordinator database file, and restart with the device powered and close to the coordinator. If the entry is still missing, re-pair once more and confirm the database file timestamp changes. Keep the backup until the device survives two restarts.

A **zigbee2mqtt device unavailable after restart** usually means the pairing never persisted, not that the hardware failed. If the log still shows no interview after a clean re-pair,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with the log excerpt and coordinator model.
