---
title: "Zigbee2MQTT MQTT Connection Failed: Fix Broker Publishing"
description: "Troubleshoot Zigbee2MQTT MQTT connection failed with a USB coordinator and new device. Check broker settings, credentials, and network, then verify with mosquitto_sub."
seo_title: "Zigbee2MQTT MQTT Connection Failed: Broker Publishing Fix"
seo_description: "Troubleshoot Zigbee2MQTT MQTT connection failed with a USB coordinator and new device. Check broker settings, credentials, and network, then verify with mosquitto_sub."
keywords:
  - "zigbee2mqtt mqtt connection failed"
date: 2026-11-15T19:23:48+08:00
publishDate: 2026-11-15T19:23:48+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have paired a new Zigbee device with your USB coordinator, but Zigbee2MQTT reports that it cannot reach the MQTT broker, so entities stay unavailable.

## Check the Broker Address and Port

Open your Zigbee2MQTT configuration and confirm the mqtt server value. It should match the broker host exactly, for example mqtt://192.168.1.50:1883. If the broker runs on the same machine, localhost is fine only when Zigbee2MQTT is not containerized. A wrong IP or port is the most common cause of a **zigbee2mqtt mqtt connection failed** message. After any change, restart Zigbee2MQTT and watch the log for a connection line.

## Verify Credentials and Access

If your broker requires authentication, ensure the username and password in the configuration are correct and that the account can publish. A rejected login usually appears as a connection refused or not authorized error. Also confirm the broker is running: from another terminal, run `mosquitto_sub -h <broker-ip> -p 1883 -t '#' -v` and check that it connects without an error. If that command fails, the problem is the broker, not Zigbee2MQTT.

## Run a Verification Test

Restart Zigbee2MQTT and inspect the first lines of its log. A successful start shows a connected message and then device state topics. In a second terminal, subscribe to `zigbee2mqtt/#` and confirm messages appear when you toggle the new device. If the log still shows a connection failure, stop Zigbee2MQTT, correct one setting at a time, and restart.

## Rollback and Recovery

If a recent configuration edit caused the failure, restore the previous configuration file from backup and restart. Keep a copy of the working file before further changes so you can revert quickly.

If the checks above do not resolve it,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and broker settings.
