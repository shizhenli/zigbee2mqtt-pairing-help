---
title: "Zigbee2MQTT Router Not Joining: Empty Network Map Fix"
description: "Troubleshoot an empty Zigbee2MQTT network map when a new router won't join. Check coordinator link, permit join, and router pairing mode to restore the map."
seo_title: "Zigbee2MQTT Router Not Joining: Empty Network Map Fix"
seo_description: "Troubleshoot an empty Zigbee2MQTT network map when a new router won't join. Check coordinator link, permit join, and router pairing mode to restore the map."
keywords:
  - "zigbee2mqtt router not joining"
date: 2026-11-23T09:13:20+08:00
publishDate: 2026-11-23T09:13:20+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've added a new Zigbee router, but the network map in Zigbee2MQTT shows nothing—not even the coordinator—so you can't confirm whether the router joined.

## Check the coordinator link first

An empty map usually means Zigbee2MQTT isn't receiving network data from the coordinator. Open the Zigbee2MQTT web interface and look at the top status bar. If it shows "Coordinator: disconnected" or the map page is blank with no nodes, the USB adapter isn't communicating. Verify the USB coordinator is firmly seated, try a different USB port (preferably USB 2.0), and confirm the correct serial port in your configuration. Restart Zigbee2MQTT. If the coordinator still doesn't appear, the issue is the adapter connection, not the router.

## Confirm permit join and router mode

If the coordinator is connected but the map remains empty, enable permit join (usually via the "Permit join" button or MQTT command). Then put the router into pairing mode per its manual—often a long press until an LED blinks. Watch the Zigbee2MQTT logs for join messages. No log entries mean the router isn't transmitting; check its battery or power and repeat pairing mode. If you see join attempts but no map update, the **zigbee2mqtt router not joining** may be due to incompatible firmware or a router that needs a factory reset before pairing.

## Verification test

After a successful join, open the network map again. You should see the coordinator and the new router as a node, with a line connecting them. If the map is still empty, restart Zigbee2MQTT and refresh the map page. A populated map confirms the fix.

## Rollback and recovery

If changes make things worse, restore your previous configuration.yaml from backup and restart. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and adapter model.
