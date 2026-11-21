---
title: "Zigbee2MQTT Permit Join Runs but No Device Appears: A Focused Fix"
description: "Permit join runs but your new Zigbee device never appears in Zigbee2MQTT? Follow these focused checks to diagnose and restore pairing."
seo_title: "Zigbee2MQTT Permit Join Finds No Device: Troubleshooting Steps"
seo_description: "Permit join runs but your new Zigbee device never appears in Zigbee2MQTT? Follow these focused checks to diagnose and restore pairing."
keywords:
  - "zigbee2mqtt permit join"
date: 2026-11-21T17:06:21+08:00
publishDate: 2026-11-21T17:06:21+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have started permit join in Zigbee2MQTT, but your new Zigbee device never shows up in the devices list.

## Check Coordinator and Network Status

First, confirm your USB coordinator is online and responding. In Zigbee2MQTT, open the Logs tab and look for recent coordinator messages. If you see errors like "Coordinator not found" or repeated timeouts, the coordinator may be disconnected or underpowered. Try a different USB port (preferably USB 2.0) and avoid unpowered hubs. Also verify that the **zigbee2mqtt permit join** window is actually open: the permit join button should show a countdown or "Disable join" state. If it closes immediately, check your configuration for `permit_join: false` and set it to `true` temporarily.

## Inspect Device and Interference

Next, check the device itself. Ensure it is in pairing mode (usually a blinking LED) and has fresh batteries. Place it within 1–2 meters of the coordinator during pairing. If it still fails, try a different Zigbee channel to avoid Wi-Fi interference—use channels 15, 20, or 25. You can change this in `configuration.yaml` under `advanced: channel`. After changing, restart Zigbee2MQTT and retry permit join.

## Verification Test

To verify, open the Zigbee2MQTT frontend, click Permit Join, and watch the Logs tab for incoming device announcements. If you see messages like "Device announce" but no device appears, the interview may be failing—check for "Interview failed" errors. If no messages appear at all, the device is not reaching the coordinator.

## Rollback and Recovery

If changes make things worse, revert your channel or configuration changes and restart Zigbee2MQTT. If the issue persists,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and device model.

## Final Tip

Always complete one change at a time and retest permit join to isolate the cause.
