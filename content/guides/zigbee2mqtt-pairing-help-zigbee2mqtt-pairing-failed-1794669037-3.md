---
title: "Permit Join Runs but No Device Appears: Fixing Zigbee2MQTT Pairing Failure"
description: "Permit join is active but your new Zigbee device never shows up in Zigbee2MQTT. Follow these checks to diagnose the pairing failure and restore discovery."
seo_title: "Zigbee2MQTT Pairing Failed: When Permit Join Finds Nothing"
seo_description: "Permit join is active but your new Zigbee device never shows up in Zigbee2MQTT. Follow these checks to diagnose the pairing failure and restore discovery."
keywords:
  - "zigbee2mqtt pairing failed"
date: 2026-11-23T12:13:39+08:00
publishDate: 2026-11-23T12:13:39+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have started permit join in Zigbee2MQTT, but your new Zigbee device never appears in the devices list, leaving you stuck at the pairing step.

## Confirm Permit Join Is Actually Active

Open the Zigbee2MQTT frontend and check that the permit join countdown is running. If it shows zero or has stopped, click Permit join again and watch the timer. A running timer means the coordinator is accepting joins; if it stops immediately, your coordinator may be busy or the MQTT connection is unstable. In that case, restart Zigbee2MQTT and retry.

## Check Device and Coordinator Proximity

Move the new device within one meter of the USB coordinator during pairing. Then put the device into pairing mode according to its manual—usually a long press until an LED blinks rapidly. Watch the Zigbee2MQTT log (Settings > Logs) for any join attempts. If you see no log entries at all, the device is not transmitting or is on a different channel. Verify the coordinator channel in your configuration and ensure the device supports it.

## Verify with a Known-Good Device

To isolate the fault, try pairing a different Zigbee device that previously worked. If it also fails, the problem is with the coordinator or permit join state; if it succeeds, the new device is likely defective or not in pairing mode. This is a controlled test to confirm where the **zigbee2mqtt pairing failed**.

## Rollback and Recovery

If you changed any settings, revert them before further testing. Restart Zigbee2MQTT and the coordinator, then attempt pairing once more. If the device still does not appear, consult the device manual for a reset procedure and try again.

For personalized diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
