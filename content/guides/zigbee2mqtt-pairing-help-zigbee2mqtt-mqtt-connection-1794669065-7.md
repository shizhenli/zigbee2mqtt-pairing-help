---
title: "Zigbee2MQTT MQTT Connection Fails: Diagnose Broker Publishing Before You Reset Anything"
description: "Zigbee2MQTT cannot publish to the broker and entities stay unavailable. Follow these checks to diagnose the MQTT connection failure and restore publishing."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
seo_description: "Zigbee2MQTT cannot publish to the broker and entities stay unavailable. Follow these checks to diagnose the MQTT connection failure and restore publishing."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-24T11:13:39+08:00
publishDate: 2026-11-24T11:13:39+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You paired a new Zigbee device with your USB coordinator, but Zigbee2MQTT stops at the mqtt connection fails step and entities remain unavailable.

## Check the Broker Address and Port
Open your Zigbee2MQTT configuration and confirm the mqtt server value matches the broker's actual host and port. A common mistake is using localhost when Zigbee2MQTT runs in a container, where localhost points to the container itself. Use the broker's LAN IP or service name instead. If the port is not 1883, verify it explicitly. After saving, restart Zigbee2MQTT and watch the log for a connection refused or timeout message; either means the address or port is wrong.

## Verify Credentials and Permissions
Check the username and password in the same mqtt section. Test them with a separate MQTT client such as mosquitto_sub against the same broker. If that client connects but Zigbee2MQTT does not, the credentials in the config are stale or contain a typo. If the client is also rejected, fix the broker's user permissions before touching Zigbee2MQTT again.

## Confirm the Broker Is Reachable
From the host running Zigbee2MQTT, run a TCP check to the broker port. A refused connection means the broker is down or firewalled; a timeout suggests network isolation. Resolve that first, because no Zigbee2MQTT setting can compensate for an unreachable broker.

## Verification Test
Restart Zigbee2MQTT and confirm the log shows a successful broker connection, then publish a test message to the base topic and subscribe to it from another client. You should see the message arrive, and entities should become available within a minute.

## Rollback Note
If changes make things worse, restore your previous configuration file and restart. Keep a backup before editing.

If the **zigbee2mqtt mqtt connection** still fails after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and broker details.
