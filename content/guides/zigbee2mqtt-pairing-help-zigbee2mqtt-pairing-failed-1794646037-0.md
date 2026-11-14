---
title: "Zigbee2MQTT Pairing Failed: When Permit Join Never Finds a Device"
description: "Troubleshoot Zigbee2MQTT when permit join runs but a new device never appears. Check coordinator link, channel, and device reset, then verify with a controlled test."
seo_title: "Zigbee2MQTT Pairing Failed: Permit Join Finds No Device"
seo_description: "Troubleshoot Zigbee2MQTT when permit join runs but a new device never appears. Check coordinator link, channel, and device reset, then verify with a controlled test."
keywords:
  - "zigbee2mqtt pairing failed"
date: 2026-11-14T20:04:28+08:00
publishDate: 2026-11-14T20:04:28+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You started permit join in Zigbee2MQTT, but your new Zigbee device never appears, so pairing cannot proceed.

## Confirm permit join is actually active
Open the Zigbee2MQTT frontend and check that permit join shows a countdown or an enabled state. If it shows disabled, enable it again and watch the countdown. A countdown that expires immediately means the request did not reach the coordinator; restart Zigbee2MQTT and retry once.

## Check the coordinator link
In the frontend, open the coordinator or network page and confirm the USB coordinator is online. If it is offline or the serial port is missing, stop here: reseat the USB cable, confirm the correct port in configuration, and restart the add-on or service. Pairing cannot work without a healthy coordinator.

## Rule out channel and interference
Verify the Zigbee channel in settings and compare it with your Wi-Fi channel. If they overlap, change the Zigbee channel, restart, and retry permit join. Keep the device within one meter of the coordinator during this test.

## Reset the device correctly
Put the device into pairing mode using its documented reset procedure, such as holding the button until the LED blinks. Watch the Zigbee2MQTT log during the attempt. If the log shows no incoming message at all, the device is not transmitting or is out of range; try a fresh battery and reset again.

## Verification test
Enable permit join, reset one known-good device, and watch for it to appear within two minutes. If it appears, the original device needs a different reset sequence. If nothing appears, the coordinator link or channel is still the problem, which confirms a **zigbee2mqtt pairing failed** condition rather than a device fault.

## Rollback and recovery
If changes made things worse, restore your previous channel and serial settings, restart Zigbee2MQTT, and confirm existing devices still report. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
