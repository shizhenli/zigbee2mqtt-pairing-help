---
title: "Zigbee2MQTT MQTT Connection Failed: When the Broker Refuses Publishing"
description: "Troubleshoot Zigbee2MQTT when the MQTT connection fails and entities stay unavailable. Check broker credentials, host, port, and verification steps."
seo_title: "Zigbee2MQTT MQTT Connection Failed: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT when the MQTT connection fails and entities stay unavailable. Check broker credentials, host, port, and verification steps."
keywords:
  - "zigbee2mqtt mqtt connection failed"
date: 2026-11-21T17:09:23+08:00
publishDate: 2026-11-21T17:09:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have Zigbee2MQTT running with a USB coordinator and a new Zigbee device, but at the MQTT connection step it fails before you can complete a controlled diagnosis, leaving entities unavailable.

## Confirm the Broker Settings

Open your Zigbee2MQTT configuration and check the mqtt section. Verify the server address matches your broker's IP or hostname and port (usually 1883, or 8883 for TLS). Confirm the username and password are correct and that the broker is running. A common mistake is using localhost when Zigbee2MQTT runs in a container or on a different machine. If the broker logs show authentication errors, the credentials are wrong. If they show connection refused, the host or port is wrong or the broker is down.

## Test the Connection Directly

From the same machine running Zigbee2MQTT, use an MQTT client to publish a test message to the broker with the same credentials. For example, run mosquitto_pub -h <broker-ip> -p 1883 -u <user> -P <password> -t test -m hello. If this fails, the problem is outside Zigbee2MQTT. If it succeeds, restart Zigbee2MQTT and watch the logs for the exact error. A successful test but failed Zigbee2MQTT connection usually points to a configuration typo or a TLS mismatch.

## Verify and Recover

After correcting the settings, restart Zigbee2MQTT and confirm the log shows a successful MQTT connection. Then check that entities become available in your home automation platform. If the connection still fails, revert to your last known working configuration backup before making further changes. This restores a stable state so you can compare differences.

If the **zigbee2mqtt mqtt connection failed** persists after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration details.
