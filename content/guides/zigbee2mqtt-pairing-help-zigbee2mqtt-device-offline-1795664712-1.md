---
title: "Zigbee2MQTT Device Offline After Service Restart: Restore Availability"
description: "Troubleshoot a Zigbee2MQTT device that becomes unavailable after a service restart. Check coordinator reconnection, MQTT state, and device interview to restore availability."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "Troubleshoot a Zigbee2MQTT device that becomes unavailable after a service restart. Check coordinator reconnection, MQTT state, and device interview to restore availability."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-28T22:32:18+08:00
publishDate: 2026-11-28T22:32:18+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or the MQTT broker, and now every entity from your new Zigbee device shows as unavailable, leaving you unsure whether the device dropped off or the service simply hasn't reconnected.

## Confirm the coordinator reconnected

Open the Zigbee2MQTT log and look for the line stating the coordinator firmware and the serial port path. If you see repeated connection errors or a missing port, the USB coordinator did not come back after the restart. Unplug and replug the coordinator, then restart Zigbee2MQTT. A successful start shows the coordinator version and no retry loop.

## Check the device's last-seen state

In the Zigbee2MQTT frontend, open the device page. If last_seen is recent and the device still shows unavailable, the issue is MQTT state, not the radio. Restart the broker and watch the Zigbee2MQTT log for a successful MQTT connect message. If last_seen is stale, the device itself is not reporting.

## Re-interview the device

With the device powered and in range, press its pairing button once to wake it, then trigger interview from the device page. Watch the log for interview completion. If the interview stalls, the device is not responding and may need a battery check or a re-pair.

## Verification test

After the steps above, toggle the device physically or via the frontend and confirm the state updates in Zigbee2MQTT and your home automation. A state change within a few seconds confirms recovery. If entities remain unavailable, the **zigbee2mqtt device offline** condition persists and needs deeper log review.

## Rollback and recovery

If changes made during diagnosis worsen the issue, restore your previous configuration.yaml and database.db backup, then restart. Keep the coordinator on a powered USB hub to avoid reconnection drops.

If the device still does not return,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and device model.
