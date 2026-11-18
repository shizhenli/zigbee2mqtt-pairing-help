---
title: "Zigbee2MQTT Router Not Joining: Why the Network Map Stays Empty"
description: "Troubleshoot a Zigbee2MQTT router that won't join when the network map shows no coordinator or routers. Step-by-step checks and a verification test."
seo_title: "Fix Zigbee2MQTT Router Not Joining: Empty Network Map"
seo_description: "Troubleshoot a Zigbee2MQTT router that won't join when the network map shows no coordinator or routers. Step-by-step checks and a verification test."
keywords:
  - "zigbee2mqtt router not joining"
date: 2026-11-18T11:31:30+08:00
publishDate: 2026-11-18T11:31:30+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've plugged in a new Zigbee router, but Zigbee2MQTT's network map shows nothing—no coordinator, no routers—and you're stuck before you can diagnose further.

## Confirm the coordinator is actually online

Open the Zigbee2MQTT frontend and check the coordinator status. If it shows offline or the serial port is missing, the map will always be empty. Re-seat the USB coordinator, confirm the correct port in configuration.yaml, and restart Zigbee2MQTT. A healthy coordinator shows as online with a recent last_seen timestamp.

## Check permit join and router power

Routers must be in pairing mode while permit join is active. In the frontend, enable permit join for all, then power-cycle the router (unplug for ten seconds, plug back in). Watch the log for interview messages. If you see nothing, the router isn't transmitting—try a different outlet away from USB 3.0 ports and metal enclosures.

## Rule out interference and distance

Place the router within a few meters of the coordinator during pairing. USB 3.0 hubs and Wi-Fi 2.4 GHz routers cause Zigbee interference; use a short USB extension cable to move the coordinator away from the host. If the map remains empty after these checks, the issue is likely coordinator-side, not the router—this is a common **zigbee2mqtt router not joining** trap.

## Verification test

After pairing, open the network map and refresh. You should see the coordinator and the new router as a connected node. Then power off the router, wait, and power it on—it should reappear within a minute. If the map still shows nothing, the coordinator isn't forming a network.

## Rollback and recovery

If changes make things worse, restore your previous configuration.yaml and restart. Remove the failed router entry from the frontend before retrying. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
