---
title: "Zigbee2MQTT Pairing Failed: Diagnose a Silent Permit Join"
description: "Permit join runs but your new Zigbee device never appears? Follow these checks to diagnose a silent pairing failure and restore detection."
seo_title: "Zigbee2MQTT Pairing Failed? Fix Permit Join Not Finding Devices"
seo_description: "Permit join runs but your new Zigbee device never appears? Follow these checks to diagnose a silent pairing failure and restore detection."
keywords:
  - "zigbee2mqtt pairing failed"
date: 2026-11-21T17:12:23+08:00
publishDate: 2026-11-21T17:12:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

**zigbee2mqtt pairing failed**. You start permit join in Zigbee2MQTT, wait, and the new device never shows up—so pairing has silently failed.

## Check Coordinator and Network State

First, confirm the coordinator is actually allowing joins. Open the Zigbee2MQTT frontend and look at the permit join countdown. If it is not counting down, the command did not reach the coordinator. Restart Zigbee2MQTT and watch the log for a line confirming permit join is enabled. A missing confirmation means the coordinator is not in pairing mode.

Next, check the device itself. Most Zigbee devices need a factory reset or a long button hold before they broadcast. Verify the battery is fresh and the reset sequence matches the manual. A device that is already paired to another network will not join until reset.

## Interpret the Log

With debug logging on, trigger pairing again. If you see no incoming messages from the device, it is not transmitting or is out of range. If you see messages but no interview, the device is visible but not completing the handshake. This distinction tells you whether to move the device closer or investigate interference.

## Verification Test

Place the device within one meter of the coordinator, start permit join, and reset the device. Watch for it to appear in the device list. If it joins at close range, the original failure was range or interference. If it still does not appear, the coordinator or device is the likely fault.

## Recovery Note

If you changed coordinator settings or firmware during diagnosis, restore your previous configuration and restart Zigbee2MQTT before returning the device to its intended location.

If these checks leave you stuck,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
