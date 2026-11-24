---
title: "Zigbee2MQTT Permit Join Runs but the Device Never Appears: A Focused Fix"
description: "Permit join runs but your new Zigbee device never shows up in Zigbee2MQTT? Follow these focused checks to diagnose the join window, coordinator link, and device state."
seo_title: "Zigbee2MQTT Permit Join: When the Device Never Appears"
seo_description: "Permit join runs but your new Zigbee device never shows up in Zigbee2MQTT? Follow these focused checks to diagnose the join window, coordinator link, and device state."
keywords:
  - "zigbee2mqtt permit join"
date: 2026-11-24T08:13:27+08:00
publishDate: 2026-11-24T08:13:27+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You started **zigbee2mqtt permit join**, waited, and the new device never appeared in the interface. That usually means the join window closed before the device sent its request, or the coordinator never heard it. Work through these checks in order and note each result.

## Confirm the join window is actually open

Open the Zigbee2MQTT frontend and check the permit join countdown. It should show a live timer (typically 254 seconds). If it shows 0 or is not counting down, the command did not reach the coordinator. Restart Zigbee2MQTT, then enable permit join again and watch the log for a line confirming the permit join was set. No confirmation line means the MQTT command path is broken, not the device.

## Check the coordinator link and device state

In the log, look for coordinator startup errors or repeated 'adapter disconnected' messages. A USB coordinator that re-enumerated after a reboot will not accept joins. Also confirm the new device is in pairing mode: most require a long press until an LED blinks rapidly. A slow blink or solid light means it is not advertising. Keep the device within one meter of the coordinator during this test.

## Verification test

Put the device in pairing mode first, then enable permit join for 254 seconds. Watch the log for an incoming 'device joined' or interview message. If the log stays silent, the radio path is the problem; if a join appears but the interview stalls, the device is reachable and the issue is elsewhere.

## Rollback and recovery

If changes make things worse, disable permit join, restart Zigbee2MQTT, and re-enable it once. Do not leave permit join open indefinitely; close it after the test to avoid unwanted joins. If the log still shows nothing after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and coordinator model.
