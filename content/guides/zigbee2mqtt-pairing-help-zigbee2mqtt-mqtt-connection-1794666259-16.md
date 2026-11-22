---
title: "Zigbee2MQTT MQTT Connection Fails: Restore Broker Publishing"
description: "Troubleshoot Zigbee2MQTT MQTT connection failures when publishing to the broker stops and entities go unavailable. Step-by-step checks and verification."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT MQTT connection failures when publishing to the broker stops and entities go unavailable. Step-by-step checks and verification."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-22T10:13:36+08:00
publishDate: 2026-11-22T10:13:36+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've paired a new Zigbee device with your USB coordinator, but Zigbee2MQTT can't publish to the broker and entities stay unavailable. This points to a **zigbee2mqtt mqtt connection** problem, not the device itself.

## Check the MQTT Broker Reachability

First, confirm the broker is running and reachable from the Zigbee2MQTT host. From a terminal on that machine, run `nc -zv <broker-host> 1883` (or 8883 for TLS). A successful connection prints "succeeded" or "open"; a timeout or refused connection means the broker isn't listening or a firewall blocks the port. If it fails, start the broker or open the port before touching Zigbee2MQTT.

## Verify Zigbee2MQTT's Broker Settings

Open your configuration.yaml and inspect the mqtt section: server, user, password, and base_topic. The server must match the broker's host and port exactly. If authentication is enabled, confirm the username and password are correct; a wrong password causes repeated connection refusals in the log. Also check that base_topic is not empty and contains no spaces. After any change, restart Zigbee2MQTT and watch the log for "Connected to MQTT server" versus "MQTT error".

## Test Publishing Directly

Use an MQTT client such as mosquitto_pub to publish a test message to your base_topic, for example `mosquitto_pub -h <broker-host> -t zigbee2mqtt/bridge/state -m online`. If the broker accepts it, the broker side is healthy and the fault is in Zigbee2MQTT's credentials or network path. If it fails, fix broker access first.

## Verify the Fix

Restart Zigbee2MQTT and confirm the log shows a successful MQTT connection. Then check that entities become available in your home automation platform and that a state change on the new device appears. If entities remain unavailable, recheck the base_topic and retained messages.

## Rollback and Recovery

If a recent configuration change caused the failure, restore the previous configuration.yaml from backup and restart. Keep the old file until the connection is stable. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
