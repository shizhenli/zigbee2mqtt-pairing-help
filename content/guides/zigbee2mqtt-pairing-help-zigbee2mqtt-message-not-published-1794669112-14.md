---
title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails"
description: "Troubleshoot Zigbee2MQTT when messages are not published and MQTT connection fails. Step-by-step checks for broker settings, logs, and recovery."
seo_title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails"
seo_description: "Troubleshoot Zigbee2MQTT when messages are not published and MQTT connection fails. Step-by-step checks for broker settings, logs, and recovery."
keywords:
  - "zigbee2mqtt message not published"
date: 2026-11-25T11:13:27+08:00
publishDate: 2026-11-25T11:13:27+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have Zigbee2MQTT with a USB coordinator and a new Zigbee device, but at the MQTT connection fails step, Zigbee2MQTT cannot publish to the broker and entities stay unavailable.

## Check the MQTT Broker Settings

Open your Zigbee2MQTT configuration.yaml and verify the mqtt section: server, user, password, and base_topic. The server must match your broker's host and port exactly (for example, mqtt://192.168.1.10:1883). If you use a username and password, confirm they are correct and that the broker allows that user to publish and subscribe. A common mistake is a trailing slash or wrong protocol. After any change, restart Zigbee2MQTT.

## Read the Logs for the Exact Error

Start Zigbee2MQTT and watch the log output. Look for lines containing "MQTT" or "connect". If you see "Connection refused", the broker is not reachable at that address or port. If you see "Not authorized", the credentials are wrong or the user lacks permissions. If you see "Client has already connected", another instance is using the same client ID. Interpret each message literally before changing anything else.

## Run a Verification Test

From the Zigbee2MQTT host, use a terminal to subscribe to the base topic: mosquitto_sub -h <broker_ip> -p 1883 -u <user> -P <password> -t 'zigbee2mqtt/#' -v. Then trigger your new device (press its pairing button). If no messages appear, the **zigbee2mqtt message not published** problem is confirmed at the broker connection level, not the device. If messages appear, the issue is downstream in your home automation platform.

## Rollback and Recovery

If a recent configuration change caused this, restore the previous configuration.yaml from backup and restart. If you cannot identify the cause, revert to a known-good broker setting and test again. For persistent cases,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and configuration details.
