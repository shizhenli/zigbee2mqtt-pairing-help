---
title: "Zigbee2MQTT Permit Join Runs but No Device Appears: A Controlled Diagnosis"
description: "Permit join is active but your new Zigbee device never shows up in Zigbee2MQTT? Follow these technician checks to isolate the cause and restore pairing."
seo_title: "Zigbee2MQTT Permit Join Never Finds a Device: Fix It Step by Step"
seo_description: "Permit join is active but your new Zigbee device never shows up in Zigbee2MQTT? Follow these technician checks to isolate the cause and restore pairing."
keywords:
  - "zigbee2mqtt permit join"
date: 2026-11-21T17:12:23+08:00
publishDate: 2026-11-21T17:12:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

## Check the permit join window and coordinator state

You enabled **zigbee2mqtt permit join**, but the new device never appears in the interface. First, confirm the window is actually open: in the Zigbee2MQTT frontend, the permit join countdown should be visible and the coordinator status should read online. If the countdown expired, re-enable it and watch for the exact remaining seconds. Next, open the Logs tab and look for `z2m: Zigbee: allowing new devices to join` at the moment you enable it. If that line is missing, the command never reached the coordinator.

## Verify the device is in pairing mode

Put the device within one meter of the coordinator and follow its manual: hold the pair button until the LED blinks rapidly, then release. A slow blink or single flash usually means it is not in pairing mode. Check the battery polarity and voltage; a weak cell can power the LED but not the radio. If the device was previously paired to another hub, factory-reset it before retrying.

## Rule out interference and channel mismatch

Open the Settings tab and note the Zigbee channel. Channels 11–14 overlap Wi-Fi 1–11 in some regions; if your router sits on the same band, move the coordinator with a USB extension cable away from the router and USB 3.0 ports. Then check the Logs for `interview` or `DeviceAnnounce` lines during the join window. No lines at all points to a radio or range problem; repeated failed interviews point to a device or firmware issue.

## Verification test

Add a known-good Zigbee device, such as a spare sensor, while permit join is open. If it joins and interviews cleanly, the coordinator and network are healthy, and the original device is the fault. If the known-good device also fails, the coordinator or channel is the problem.

## Rollback and recovery

If you changed the channel or coordinator settings, restore the previous configuration and restart Zigbee2MQTT before further testing. If the network remains unresponsive,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and coordinator model.
