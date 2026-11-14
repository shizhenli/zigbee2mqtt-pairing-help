---
title: "Zigbee2MQTT Permit Join: Why Your New Device Never Appears"
description: "Permit join runs but your new Zigbee device never shows up in Zigbee2MQTT? Follow these checks to diagnose the coordinator, network, and device state."
seo_title: "Zigbee2MQTT permit join never finds a device: fix it step by step"
seo_description: "Permit join runs but your new Zigbee device never shows up in Zigbee2MQTT? Follow these checks to diagnose the coordinator, network, and device state."
keywords:
  - "zigbee2mqtt permit join"
date: 2026-11-14T20:04:28+08:00
publishDate: 2026-11-14T20:04:28+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You started permit join in Zigbee2MQTT, put your new Zigbee device into pairing mode, and waited—but the device never appeared in the dashboard.

## Check the permit join window and coordinator link

First, confirm the permit join window is actually open. In the Zigbee2MQTT frontend, the permit join button should show a countdown or active state. If it closed after 254 seconds, reopen it and keep the page visible. Next, verify the USB coordinator is responding: check the Zigbee2MQTT logs for recent coordinator messages and no "adapter disconnected" errors. A coordinator that dropped off USB will accept the permit join command but never hear devices.

## Verify device pairing mode and distance

Put the device back into pairing mode according to its manual—usually a long press until an LED blinks rapidly. Place it within one meter of the coordinator or a known-good router during this test. If the device previously joined another network, perform a factory reset before retrying. Watch the Zigbee2MQTT log while pairing; a device that is transmitting should produce at least one join or interview line.

## Run a controlled verification test

With the coordinator confirmed and the device reset, start **zigbee2mqtt permit join** again and watch the log for 60 seconds. If no join line appears, try a second known-working Zigbee device. If that device also fails, the issue is the coordinator or USB path; if it succeeds, the original device is the problem.

## Rollback and recovery

If you changed coordinator firmware or USB port, revert to the previous working setup and restart Zigbee2MQTT before further testing. If the coordinator remains unresponsive, stop permit join and power-cycle the USB coordinator, then restart the add-on. For deeper diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
