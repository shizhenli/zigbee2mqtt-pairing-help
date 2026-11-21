---
title: "Zigbee2MQTT MQTT Connection Fails: Diagnose Broker Publishing Before Pairing"
description: "Troubleshoot Zigbee2MQTT MQTT connection failures when publishing to the broker fails and entities stay unavailable. Step-by-step checks and verification."
seo_title: "Zigbee2MQTT MQTT Connection Fails: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT MQTT connection failures when publishing to the broker fails and entities stay unavailable. Step-by-step checks and verification."
keywords:
  - "zigbee2mqtt mqtt connection"
date: 2026-11-21T17:06:21+08:00
publishDate: 2026-11-21T17:06:21+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You're setting up Zigbee2MQTT with a USB coordinator and a new Zigbee device, but at the MQTT connection step it fails before you can complete a controlled diagnosis, so Zigbee2MQTT cannot publish to the broker and entities stay unavailable.

## Check the Broker Address and Port

Open your Zigbee2MQTT configuration and confirm the MQTT server value. It must match the broker's actual host and port, for example `mqtt://192.168.1.50:1883`. If the broker runs on the same machine as Zigbee2MQTT, use `mqtt://localhost:1883` or the loopback address. A wrong IP or a missing port is the most common cause of a failed publish. After any change, restart Zigbee2MQTT and watch the log for a connection line.

## Verify Credentials and Access

If your broker requires authentication, check that the username and password in the configuration are correct and that the account has publish and subscribe rights. Test the same credentials with a separate MQTT client. If that client connects and publishes, the broker is reachable and the fault is in Zigbee2MQTT's settings. If it also fails, fix the broker account before continuing.

## Confirm the Broker Is Listening

From the Zigbee2MQTT host, run `nc -zv <broker-ip> 1883` or `telnet <broker-ip> 1883`. A successful connection means the port is open. A refused or timed-out result points to a firewall, a stopped broker, or a wrong port. Check the broker service status and any firewall rules on both machines.

## Verification Test

Restart Zigbee2MQTT and inspect the log for a successful MQTT connection message. Then publish a test message to `zigbee2mqtt/bridge/state` from an MQTT client and confirm it appears. If entities remain unavailable, the **zigbee2mqtt mqtt connection** is still not established.

## Rollback and Recovery

If a recent configuration edit caused the failure, restore the previous `configuration.yaml` from backup and restart. Keep a known-good copy before further changes. If the checks above do not resolve the publish failure,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and broker details.
