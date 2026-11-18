---
title: "Zigbee2MQTT MQTT Connection Failed: Diagnose Broker Publishing Before Pairing"
description: "Zigbee2MQTT cannot publish to the broker and entities stay unavailable. Check broker settings, credentials, and network reachability to restore MQTT publishing."
seo_title: "Zigbee2MQTT MQTT Connection Failed: Fix Broker Publishing"
seo_description: "Zigbee2MQTT cannot publish to the broker and entities stay unavailable. Check broker settings, credentials, and network reachability to restore MQTT publishing."
keywords:
  - "zigbee2mqtt mqtt connection failed"
date: 2026-11-18T08:13:38+08:00
publishDate: 2026-11-18T08:13:38+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are pairing a new Zigbee device with a USB coordinator, but Zigbee2MQTT stops at the MQTT connection step and entities remain unavailable. This points to a broker publishing failure, not a pairing fault.

## Check Broker Settings and Credentials

Open your Zigbee2MQTT configuration and verify the mqtt section. Confirm the server address matches your broker host and port, for example mqtt://192.168.1.10:1883. Check that user and password are correct and that the broker allows this client. A wrong port or typo in credentials will block publishing. If your broker uses TLS, ensure the protocol and certificates are configured. After any change, restart Zigbee2MQTT and watch the log for a connection refused or not authorized message. That exact result means the broker rejected the client, so fix credentials or access control before retrying.

## Verify Network Reachability

From the machine running Zigbee2MQTT, test the broker port with a simple TCP check such as nc -vz broker-ip 1883. A successful connection confirms the network path. If it fails, check firewall rules, Docker network settings, or whether the broker is listening on the expected interface. This isolates a **zigbee2mqtt mqtt connection failed** condition from a coordinator or device issue.

## Verification Test

Publish a test message to the Zigbee2MQTT base topic using an MQTT client, then confirm Zigbee2MQTT logs show a successful connection and entities become available. If the log still shows publish errors, the broker configuration remains the cause.

## Rollback and Recovery

If a recent configuration change caused the failure, restore the previous working mqtt section from backup and restart. Keep the coordinator connected; do not re-pair the device until MQTT publishing is stable. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
