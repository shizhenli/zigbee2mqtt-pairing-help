---
title: "After a Zigbee2MQTT Restart, All Entities Show Unavailable: What to Check First"
description: "All Zigbee entities turn unavailable after a Zigbee2MQTT or broker restart? Follow these checks to confirm whether the device is truly offline and restore availability."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "All Zigbee entities turn unavailable after a Zigbee2MQTT or broker restart? Follow these checks to confirm whether the device is truly offline and restore availability."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-25T08:13:28+08:00
publishDate: 2026-11-25T08:13:28+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or your MQTT broker, and now every entity from your new Zigbee device shows unavailable, leaving you unsure whether the device dropped off or the service simply hasn't caught up.

## Confirm the service is actually running

Open the Zigbee2MQTT log and look for the startup sequence: coordinator detected, network parameters loaded, and MQTT connected. If the log stops before "MQTT connected," the broker link is the problem, not the device. If it reaches "MQTT connected" but no device messages follow, continue below.

## Check the device's last-seen state

In the Zigbee2MQTT frontend, open the device page and note the last-seen timestamp and link quality. A timestamp older than the restart time with a link quality of 0 or unknown means the device has not rejoined. A recent timestamp with good link quality means the device is reporting but the entity state was not republished.

## Verify the MQTT retained state

Use an MQTT client to subscribe to `zigbee2mqtt/<friendly_name>/availability`. If the retained message is `offline`, Zigbee2MQTT marked the device as a **zigbee2mqtt device offline** after the restart. If no message arrives, the broker lost the retained state during its own restart.

## Verification test

Trigger the device physically (press its button or open the contact) and watch the log for an incoming message. A new message with a fresh timestamp confirms the radio link works; then reload the Zigbee2MQTT frontend and confirm the entity returns to available.

## Rollback and recovery

If the device still does not report, power-cycle it and re-run permit join for 60 seconds. If entities remain unavailable after a second restart, restore your last working `configuration.yaml` backup before making further changes. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
