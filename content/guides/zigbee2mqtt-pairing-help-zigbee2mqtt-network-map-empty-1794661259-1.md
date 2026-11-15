---
title: "Zigbee2MQTT Network Map Empty: Why the Coordinator and Routers Don't Appear"
description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers are missing. Check LQI, adapter state, and MQTT topics, then verify with a controlled test."
seo_title: "Zigbee2MQTT Network Map Empty: Fix Missing Coordinator and Routers"
seo_description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers are missing. Check LQI, adapter state, and MQTT topics, then verify with a controlled test."
keywords:
  - "zigbee2mqtt network map empty"
date: 2026-11-15T19:23:48+08:00
publishDate: 2026-11-15T19:23:48+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and a new Zigbee device, and when you open the network map it shows nothing—no coordinator, no routers.

## Confirm what the map is actually reading

First, open the Zigbee2MQTT frontend and go to the Network tab. The map is built from link-quality data that the coordinator reports. If the coordinator is not listed, the map has no starting point. Check the Logs tab for lines containing `Coordinator` or `adapter`. A healthy start shows the adapter type and firmware version. If you see `Error: Failed to connect to the adapter` or no coordinator line at all, the USB stick is not being read—re-seat it, confirm the correct port in configuration.yaml, and restart Zigbee2MQTT.

## Check that routers are reporting links

If the coordinator appears but routers do not, the map is not receiving neighbor data. In the Devices tab, confirm each router shows a recent `last_seen` timestamp. A router that has not reported in hours will not appear on the map. Trigger a fresh report by pressing the device's pairing button once (do not re-pair). Wait two minutes, then refresh the map. If the map is still blank, the symptom is a **zigbee2mqtt network map empty** state caused by missing link data, not a broken map page.

## Verification test

Open the MQTT topic `zigbee2mqtt/bridge/networkmap` and publish `graphviz` or `raw`. A response should appear within seconds. Then return to the Network tab and confirm the coordinator node is drawn. If the topic returns data but the map stays blank, clear the browser cache and reload the frontend.

## Rollback and recovery

If changes to the adapter port or network settings caused the blank map, restore the previous configuration.yaml backup and restart. Do not re-pair devices to fix a map display issue. If the coordinator still does not appear after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and adapter model.
