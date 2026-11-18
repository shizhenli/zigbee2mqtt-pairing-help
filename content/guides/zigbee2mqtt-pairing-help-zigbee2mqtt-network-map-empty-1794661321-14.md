---
title: "Zigbee2MQTT Network Map Empty: Why the Coordinator and Routers Are Missing"
description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers do not appear. Check MQTT topics, adapter state, and map generation, then verify with a test."
seo_title: "Zigbee2MQTT Network Map Empty: Fix Missing Coordinator and Routers"
seo_description: "Troubleshoot an empty Zigbee2MQTT network map when the coordinator and routers do not appear. Check MQTT topics, adapter state, and map generation, then verify with a test."
keywords:
  - "zigbee2mqtt network map empty"
date: 2026-11-18T09:13:26+08:00
publishDate: 2026-11-18T09:13:26+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

**zigbee2mqtt network map empty**. You have Zigbee2MQTT running with a USB coordinator and a newly paired device, but the network map shows nothing at all.

## Check the basics first

Open the Zigbee2MQTT web interface and confirm the coordinator is online. Look at the top bar: it should show the coordinator name and a green status. If it shows a red or disconnected state, the map cannot render because the frontend has no live data. Next, open the Logs tab and look for errors containing "adapter" or "network map". A common cause is that the map was requested before the coordinator finished starting. Wait 30 seconds after startup, then reload the page.

## Verify the map request path

The network map is built from a request sent over MQTT. In the Zigbee2MQTT frontend, click the map icon and watch the Logs tab. You should see a line like "Requesting network map". If nothing appears, the frontend is not connected to the MQTT broker. Check that the MQTT server address and credentials in your configuration match the broker, and that the base topic is correct. If the request appears but no data returns, the coordinator may be busy. Stop Zigbee2MQTT, unplug the USB coordinator for ten seconds, plug it back in, and start the service.

## Verification test

After restarting, pair a router or use an existing mains-powered device. Open the map and wait up to one minute. You should see the coordinator in the center and at least one router linked to it. If the map remains blank, the issue is likely the coordinator firmware or a corrupted database. Back up your `database.db` file before making changes.

## Rollback and recovery

If a recent configuration change caused the problem, restore your previous `configuration.yaml` and `database.db` from backup, then restart. This returns you to a known working state. For persistent cases where the map stays empty despite correct MQTT and adapter settings,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration details.
