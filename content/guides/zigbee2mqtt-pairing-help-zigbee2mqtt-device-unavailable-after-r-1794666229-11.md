---
title: "Zigbee2MQTT Device Unavailable After Restart: Fix the Stale Entity"
description: "A focused fix for when a Zigbee2MQTT device shows unavailable after a service restart, with exact checks, a verification test, and a recovery note."
seo_title: "Zigbee2MQTT Device Unavailable After Restart — Fix It"
seo_description: "A focused fix for when a Zigbee2MQTT device shows unavailable after a service restart, with exact checks, a verification test, and a recovery note."
keywords:
  - "zigbee2mqtt device unavailable after restart"
date: 2026-11-21T17:12:23+08:00
publishDate: 2026-11-21T17:12:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the MQTT broker, and now a device that worked before shows as unavailable in Home Assistant.

## Confirm the restart is the trigger

First, separate a restart problem from a pairing problem. Open the Zigbee2MQTT frontend and check the device's last seen time. If it updated after the restart, the radio link is fine and the issue is entity state. If it did not update, the device itself is not reporting and you should re-check its battery or range before continuing.

Next, inspect the Zigbee2MQTT log for the device's IEEE address. A successful interview or a recent message means the coordinator still knows it. Look for repeated `request timeout` lines instead; those point to a radio issue, not a restart issue.

## Check the retained state path

A common cause is a stale retained MQTT message. Use an MQTT client to subscribe to `zigbee2mqtt/<friendly_name>/availability`. If it shows `offline` while the frontend shows the device as present, the retained value is wrong. Clear that retained topic, then restart Zigbee2MQTT once so it republishes the correct state.

Also confirm the device's `availability` setting in `configuration.yaml` has not been enabled with a timeout shorter than your restart window.

## Verification test

After clearing the retained topic, restart Zigbee2MQTT again and watch the entity in Home Assistant. It should return to available within one reporting interval. Trigger the device physically and confirm the state changes.

If it still fails, this is a **zigbee2mqtt device unavailable after restart** case that needs log-level inspection rather than more restarts.

## Recovery note

If clearing retained messages makes things worse, restore your previous `configuration.yaml` and database backup before retrying. For a guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
