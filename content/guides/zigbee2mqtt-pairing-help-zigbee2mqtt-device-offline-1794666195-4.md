---
title: "Zigbee2MQTT Device Offline After Pairing: Fix the Silent Drop"
description: "A focused fix for a Zigbee device that pairs but stops responding in Zigbee2MQTT. Check link quality, re-interview, and verify with a simple test."
seo_title: "Zigbee2MQTT Device Offline: Why It Stops Reporting After Pairing"
seo_description: "A focused fix for a Zigbee device that pairs but stops responding in Zigbee2MQTT. Check link quality, re-interview, and verify with a simple test."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-21T17:09:23+08:00
publishDate: 2026-11-21T17:09:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You paired a new Zigbee device with your USB coordinator, it appeared in Zigbee2MQTT, then stopped reporting state after a short time.

## Check the device's last-seen and link quality
Open the device in the Zigbee2MQTT frontend and look at the last-seen timestamp and link quality. If last-seen is recent but state is stale, the device is reachable but not sending updates. If last-seen is hours old, it has dropped off the mesh. Link quality below 20 suggests a weak path; move the device closer or add a router.

## Re-interview and confirm the model
Click the device, then Interview. Watch the log for a successful interview. If the interview completes but the device still goes quiet, the pairing is incomplete. Remove the device, permit join again, and pair it while it is within one meter of the coordinator. Confirm the model matches the supported devices list; an unrecognized model may pair but not report correctly.

## Verification test
After re-interviewing, toggle the device physically and watch the state in the frontend. Then wait ten minutes and toggle again. If both changes appear, the fix held. If the second toggle is missing, the device is still dropping and you should treat it as a **zigbee2mqtt device offline** case and check for interference or a failing battery.

## Rollback and recovery
If the device worked before a recent change, restore your previous Zigbee2MQTT configuration backup and restart the service. Remove and re-pair only after the rollback, so you do not carry a bad interview forward.

If these checks do not restore reporting,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and device model.
