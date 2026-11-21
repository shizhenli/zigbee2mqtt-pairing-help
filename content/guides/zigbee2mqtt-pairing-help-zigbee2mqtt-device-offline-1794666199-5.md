---
title: "Zigbee2MQTT Device Offline After a Service Restart"
description: "Your new Zigbee device shows unavailable after restarting Zigbee2MQTT or the broker. Follow these checks to confirm whether the device is truly offline or the state is stale."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "Your new Zigbee device shows unavailable after restarting Zigbee2MQTT or the broker. Follow these checks to confirm whether the device is truly offline or the state is stale."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-21T17:09:23+08:00
publishDate: 2026-11-21T17:09:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

## What you are seeing

You paired a new Zigbee device with your USB coordinator, restarted Zigbee2MQTT or the MQTT broker, and now every entity reports unavailable.

This usually means the restart interrupted the normal state handshake, not that the device vanished. Work through the checks below before re-pairing anything.

## Check the coordinator and network state

Open the Zigbee2MQTT frontend and confirm the coordinator shows online. In the log, look for the startup sequence completing without repeated "adapter disconnected" or "MQTT publish failed" lines. If the log stops before the network scan finishes, the restart did not complete cleanly.

Next, open the device's page and check its last seen value. A timestamp from before the restart suggests the state is stale. A fresh timestamp with unavailable entities points to a reporting or broker issue instead.

## Verify the device is reachable

Trigger the device physically, such as pressing its button or opening a contact. Watch the frontend for a state change. If the last seen value updates, the radio link is fine and only the entity state needs refreshing. If nothing changes, move the device closer to the coordinator and repeat.

## Verification test

Restart Zigbee2MQTT once more and wait two full minutes without touching any device. Then check whether entities return to their previous values. If they do, the earlier restart was simply incomplete. If they stay unavailable, treat the device as a **zigbee2mqtt device offline** case and inspect the broker connection next.

## Recovery note

If you changed any settings before the restart, revert them and restart again. Avoid removing and re-pairing the device until these checks are done, since removal discards its network keys. If the state still does not return,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt.
