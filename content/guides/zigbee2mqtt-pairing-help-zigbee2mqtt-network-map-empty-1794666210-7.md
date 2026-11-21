---
title: "Zigbee2MQTT Network Map Empty: Restore Coordinator and Router Visibility"
description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers are missing. Follow specific checks, interpret results, and verify with a test."
seo_title: "Zigbee2MQTT Network Map Empty: Fix Missing Coordinator and Routers"
seo_description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers are missing. Follow specific checks, interpret results, and verify with a test."
keywords:
  - "zigbee2mqtt network map empty"
date: 2026-11-21T17:09:23+08:00
publishDate: 2026-11-21T17:09:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and just added a new Zigbee device, but the network map shows nothing—no coordinator, no routers.

## Check the Coordinator Connection and Map Data Source

First, confirm the coordinator is online. In the Zigbee2MQTT frontend, open Settings > About. The coordinator firmware and IEEE address should be listed. If they are missing, the map cannot populate. Next, go to the Map tab and click the refresh icon. Wait 30 seconds. If the map remains blank, the issue is likely that the map data has not been generated or the frontend cannot read it.

## Verify Network Map Generation in Configuration

Open your configuration.yaml and check that `frontend` is enabled and `networkmap` is not disabled. Also ensure `permit_join` is false after pairing—leaving it true can cause map instability. Restart Zigbee2MQTT. After restart, check the logs for "Network map" entries. If you see errors like "Failed to generate network map," the coordinator may not be responding to map requests.

## Run a Verification Test

With the coordinator connected, power cycle one known router (a mains-powered Zigbee device). Wait two minutes. Refresh the map. If the router appears, the map is working and the original emptiness was a timing or cache issue. If it still does not appear, the coordinator may not be routing properly.

## Rollback and Recovery

If you recently changed coordinator firmware or USB port, revert to the previous firmware or port. Then restart Zigbee2MQTT and refresh the map. If the map remains empty, your coordinator may need a firmware reflash or the database may be corrupted. Back up `coordinator_backup.json` before any reflash.

If these steps do not resolve your **zigbee2mqtt network map empty** issue,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration.
