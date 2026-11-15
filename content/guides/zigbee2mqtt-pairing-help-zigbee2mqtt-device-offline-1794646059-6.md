---
title: "Zigbee2MQTT Device Offline After a Service Restart: Restore Availability"
description: "All entities become unavailable after Zigbee2MQTT or the broker restarts. Follow these checks to diagnose and restore the device."
seo_title: "Zigbee2MQTT Device Offline After Restart: Fix Unavailable Entities"
seo_description: "All entities become unavailable after Zigbee2MQTT or the broker restarts. Follow these checks to diagnose and restore the device."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-15T19:23:48+08:00
publishDate: 2026-11-15T19:23:48+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You restarted Zigbee2MQTT or your MQTT broker, and now every entity from your new Zigbee device shows as unavailable.

## Check the coordinator and network state

First, confirm Zigbee2MQTT started cleanly. Open the log and look for a line stating the coordinator is connected and the network is up. If you see repeated reconnect attempts or a USB error, the coordinator did not recover from the restart. Unplug the USB coordinator, wait ten seconds, plug it back into the same port, and restart Zigbee2MQTT. A clean start shows the coordinator version and no repeating errors.

## Check the device's last-seen and interview status

In the Zigbee2MQTT interface, open the device page. Check last_seen and the interview status. If last_seen is recent but entities are unavailable, the problem is between Zigbee2MQTT and the broker, not the radio. If last_seen is old or empty, the device has not rejoined the network.

## Verify MQTT broker connectivity

Restart the broker alone and watch the Zigbee2MQTT log. A healthy connection logs a successful MQTT connect and subscribe. If it fails, check the broker address, port, username, and password in configuration.yaml. A wrong port or expired credential makes every entity unavailable after a restart.

## Verification test

Trigger the device physically, such as pressing its button. Watch the log for an incoming message and confirm last_seen updates. Then toggle an entity from the interface and confirm the device responds. If both work, availability is restored.

## Rollback and recovery

If changes made during diagnosis worsened the issue, restore your previous configuration.yaml and restart Zigbee2MQTT. If the device remains a **zigbee2mqtt device offline** after these checks, re-pair it without removing it first, or consult

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt.
