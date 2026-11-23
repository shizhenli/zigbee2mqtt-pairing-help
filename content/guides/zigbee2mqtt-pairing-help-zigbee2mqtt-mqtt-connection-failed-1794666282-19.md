---
title: "Zigbee2MQTT MQTT Connection Failed: Fix Broker Publishing After Adding a Device"
description: "Troubleshoot Zigbee2MQTT MQTT connection failed after adding a new device: check broker credentials, verify publish permissions, and restore entity availability."
seo_title: "Zigbee2MQTT MQTT Connection Failed: Fix Broker Publishing"
seo_description: "Troubleshoot Zigbee2MQTT MQTT connection failed after adding a new device: check broker credentials, verify publish permissions, and restore entity availability."
keywords:
  - "zigbee2mqtt mqtt connection failed"
date: 2026-11-23T08:13:25+08:00
publishDate: 2026-11-23T08:13:25+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You added a new Zigbee device and now Zigbee2MQTT reports a **zigbee2mqtt mqtt connection failed** error, leaving entities unavailable.

## Check the Broker Connection Settings

Open your Zigbee2MQTT configuration (usually `configuration.yaml`). Under `mqtt`, confirm the `server` value matches your broker's host and port exactly, for example `mqtt://192.168.1.10:1883`. If you use TLS, the scheme must be `mqtts://`. Verify `user` and `password` are correct and have no trailing spaces. A wrong port or typo here is the most common cause of a failed publish.

## Verify Publish Permissions

Connect to your broker with a client such as MQTT Explorer using the same credentials. Try publishing a test message to `zigbee2mqtt/bridge/state`. If the broker rejects the publish, the account lacks write access to that topic. Grant publish and subscribe rights on `zigbee2mqtt/#` and restart Zigbee2MQTT.

## Run a Verification Test

After saving changes, restart the service and watch the log for `Connected to MQTT server`. Then check that `zigbee2mqtt/bridge/state` shows `online` in your broker client. Finally, confirm your new device's entity updates in Home Assistant. If the log still shows a connection error, note the exact error text before changing anything else.

## Rollback and Recovery

If the failure began after a configuration edit, restore your previous `configuration.yaml` from backup and restart. This returns you to a known working state so you can reapply changes one at a time.

If these checks do not resolve it,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and broker settings.
