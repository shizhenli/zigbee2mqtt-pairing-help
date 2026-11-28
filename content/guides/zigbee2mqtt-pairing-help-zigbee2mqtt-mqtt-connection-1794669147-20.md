---
title: "Zigbee2MQTT MQTT Connection Fails: Restore Publishing to the Broker"
description: "Troubleshoot Zigbee2MQTT MQTT connection failures when a new Zigbee device is stuck before diagnosis. Check broker settings, credentials, and network access, then verify publishing and recover safely."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT MQTT connection failures when a new Zigbee device is stuck before diagnosis. Check broker settings, credentials, and network access, then verify publishing and recover safely."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-28T22:04:35+08:00
publishDate: 2026-11-28T22:04:35+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are adding a new Zigbee device with a USB coordinator, and Zigbee2MQTT stops at the MQTT connection step, so entities never become available.

## Check the broker address and port

Open your Zigbee2MQTT configuration and confirm the mqtt server value. For a broker on the same host, use localhost or 127.0.0.1 with the correct port, usually 1883. If the broker runs elsewhere, use its LAN IP and ensure the port is reachable. A wrong host or port is the most common reason the **zigbee2mqtt mqtt connection** fails before any device interview begins.

## Verify credentials and client identity

If your broker requires authentication, confirm the username and password exactly, including case. Check that the client ID is unique; a duplicate client ID can cause the broker to reject or drop the session. After saving changes, restart Zigbee2MQTT and watch the log for a successful connection line rather than repeated reconnect attempts.

## Test publishing from the broker side

Use an MQTT client such as mosquitto_sub to subscribe to zigbee2mqtt/#. Restart Zigbee2MQTT and look for the bridge state topic. If messages appear, publishing works. If not, confirm the broker is running and that no firewall blocks the port between the Zigbee2MQTT host and the broker.

## Roll back safely

If a recent configuration edit caused the failure, restore the previous configuration file and restart. Keep a backup before further changes so you can return to a known working state.

If the log still shows connection refused or timeout errors after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your configuration and log excerpt.
