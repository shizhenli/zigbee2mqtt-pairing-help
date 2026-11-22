---
title: "Zigbee2MQTT Device Joins Then Stops Reporting: Fix the Silent Drop-Off"
description: "Your Zigbee device pairs but stops responding in Zigbee2MQTT? Diagnose the silent drop-off with link quality, interview state, and a verification test."
seo_title: "Zigbee2MQTT Device Not Responding After Pairing: Silent Drop-Off Fix"
seo_description: "Your Zigbee device pairs but stops responding in Zigbee2MQTT? Diagnose the silent drop-off with link quality, interview state, and a verification test."
keywords:
  - "zigbee2mqtt device not responding"
date: 2026-11-22T08:13:33+08:00
publishDate: 2026-11-22T08:13:33+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You paired a new Zigbee device and it joined, but after a short time it stopped reporting state, leaving you stuck at the device pairs but stops responding step.

## Confirm the device is actually silent

Open the device in Zigbee2MQTT and check the last seen timestamp. If it is older than the reporting interval you expect, the device is silent, not just slow. Then check the link quality value. A reading below 30 usually means a weak path to the coordinator. If link quality is healthy but state is frozen, move to the interview check.

## Check the interview state

In the device's About tab, confirm the interview completed. A device that joined but never finished interviewing often accepts commands briefly, then stops. If interview is incomplete, remove the device, reset it, and pair again while it sits within one metre of the USB coordinator. Keep it there until the interview finishes, then move it to its final location.

## Rule out the coordinator path

With a USB coordinator, extension cables matter. Plug the coordinator into a short USB extension cable away from the computer chassis and any USB 3.0 ports. Then restart Zigbee2MQTT and watch whether the device reports again. If it does, the original position was the problem.

## Verification test

Trigger a state change at the device, such as pressing its button or opening the contact. Watch the Zigbee2MQTT log for an incoming message. A fresh timestamp and a state update mean the path is restored. No log entry means the device is still not reaching the coordinator.

## Rollback and recovery

If nothing changes, remove the device from Zigbee2MQTT, factory reset it, and re-pair at close range. This returns you to a clean pairing state without losing your other devices. If the **zigbee2mqtt device not responding** issue persists after a clean re-pair, the coordinator or device firmware may need review.

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and link quality values.
