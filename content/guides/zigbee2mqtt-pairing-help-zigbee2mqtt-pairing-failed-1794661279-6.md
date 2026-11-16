---
title: "Zigbee2MQTT Pairing Failed: What to Check When Permit Join Finds No Device"
description: "Troubleshoot a Zigbee2MQTT pairing failure when permit join runs but the new device never appears. Check coordinator status, channel, and device reset, then verify with a test."
seo_title: "Zigbee2MQTT Pairing Failed: Permit Join Finds No Device"
seo_description: "Troubleshoot a Zigbee2MQTT pairing failure when permit join runs but the new device never appears. Check coordinator status, channel, and device reset, then verify with a test."
keywords:
  - "zigbee2mqtt pairing failed"
date: 2026-11-16T11:13:06+08:00
publishDate: 2026-11-16T11:13:06+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You enabled permit join in Zigbee2MQTT, but your new Zigbee device never appears, leaving you stuck at the permit join never finds a device step.

## Confirm permit join is actually active

Open the Zigbee2MQTT frontend and check the permit join countdown. If it shows zero or has already expired, click Permit join (all) again and watch the timer. A running countdown means the coordinator is accepting joins; a missing or instantly expiring timer points to a coordinator or configuration problem, not the device.

## Check the coordinator link and channel

In the Zigbee2MQTT logs, look for the coordinator startup line and any recent errors. If the USB coordinator is not listed or shows repeated disconnects, reseat it in a powered USB port and restart Zigbee2MQTT. Then compare the Zigbee channel in your configuration with your Wi-Fi channel; a channel overlap (for example, Zigbee 11 near Wi-Fi 1) can prevent joins. Change the Zigbee channel only if you can re-pair existing devices, and note the old value so you can roll back.

## Reset the device correctly

Put the device into pairing mode per its manual, usually a long press until an LED blinks. Keep it within a few meters of the coordinator during the attempt. If it still does not appear, remove its battery for ten seconds, replace it, and start permit join again before resetting.

## Verification test

With permit join active, reset the device once more and watch the Zigbee2MQTT log for an incoming join or interview message. If a device line appears, pairing succeeded. If nothing appears after two attempts, the join never reached the coordinator; revisit the coordinator link and channel checks. This confirms whether the failure is radio-side or device-side.

If these steps do not resolve your **zigbee2mqtt pairing failed** state,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and coordinator model.
