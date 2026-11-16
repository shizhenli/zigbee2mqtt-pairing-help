---
title: "Zigbee2MQTT Message Not Published: When the Broker Connection Fails"
description: "Troubleshoot Zigbee2MQTT when messages are not published and the MQTT connection fails. Step-by-step checks for broker settings, credentials, and network access."
seo_title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails"
seo_description: "Troubleshoot Zigbee2MQTT when messages are not published and the MQTT connection fails. Step-by-step checks for broker settings, credentials, and network access."
keywords:
  - "zigbee2mqtt message not published"
date: 2026-11-16T09:13:01+08:00
publishDate: 2026-11-16T09:13:01+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have paired a new Zigbee device, but Zigbee2MQTT cannot publish to the broker, so entities stay unavailable and you are stuck at the mqtt connection fails step.

## Confirm the Failure Point

Open the Zigbee2MQTT log and look for lines containing "MQTT" or "connect". A healthy start shows a successful connection before device interviews. If you see "Connection refused", "Not authorized", or repeated reconnect attempts, the broker link is the problem, not the device. Note the exact error text; it tells you whether this is a network, credential, or configuration issue.

## Check Broker Settings and Credentials

In configuration.yaml, verify the mqtt server address, port, user, and password. The server must be reachable from the host running Zigbee2MQTT, not just from your laptop. A common mistake is using localhost when the broker runs in another container or on another machine. Confirm the username and password match the broker's user list exactly, including case. If your broker uses TLS, ensure the port and certificate settings are correct; a plain connection to a TLS port will fail silently in some setups.

## Run a Verification Test

From the Zigbee2MQTT host, test the broker directly with a command such as mosquitto_pub to publish a test message to a topic like zigbee2mqtt/bridge/state. If that command fails with the same error, the issue is outside Zigbee2MQTT. If it succeeds, restart Zigbee2MQTT and watch the log for a clean connection. Then check that a device state topic receives updates. This isolates whether the **zigbee2mqtt message not published** symptom comes from the broker or the application.

## Rollback and Recovery

If a recent configuration change caused the failure, restore the previous configuration.yaml from backup and restart. Keep a known-good copy before editing broker settings. If the problem persists after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and configuration details.
