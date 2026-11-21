---
title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails Before Diagnosis"
description: "Troubleshoot Zigbee2MQTT when messages aren't published and the MQTT connection fails. Step-by-step checks to restore broker publishing."
seo_title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails"
seo_description: "Troubleshoot Zigbee2MQTT when messages aren't published and the MQTT connection fails. Step-by-step checks to restore broker publishing."
keywords:
  - "zigbee2mqtt message not published"
date: 2026-11-21T17:12:23+08:00
publishDate: 2026-11-21T17:12:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've paired a new Zigbee device with your USB coordinator, but Zigbee2MQTT can't publish to the broker and entities stay unavailable, stuck at the mqtt connection fails step.

## Check the MQTT Broker Connection

Open your Zigbee2MQTT log and look for lines like `MQTT connect error` or `Connection refused`. If you see `ECONNREFUSED`, the broker isn't reachable at the configured address. Verify the broker host and port in your `configuration.yaml` under `mqtt.server`. For a local Mosquitto broker, it's usually `mqtt://localhost:1883`. If Zigbee2MQTT runs in Docker, `localhost` points to the container itself, not the host—use the host's IP or the broker's service name instead. Also confirm the broker is running: `sudo systemctl status mosquitto` should show `active (running)`.

## Verify Credentials and Permissions

If the log shows `Not authorized` or `Connection refused: bad username or password`, check the `mqtt.user` and `mqtt.password` values. Test them directly with `mosquitto_sub -h <broker> -p 1883 -u <user> -P <pass> -t '#' -v`. A successful subscription prints messages; an error means the credentials or ACLs are wrong. Fix them in the broker config, restart Mosquitto, then restart Zigbee2MQTT.

## Confirm the Publish Path

Once connected, watch the log for `MQTT publish` entries. If you see `**zigbee2mqtt message not published**` warnings, the broker connection dropped mid-publish. Check for network instability or broker overload. Restart Zigbee2MQTT and re-check.

## Verification Test

After fixing the connection, publish a test message from Zigbee2MQTT's frontend (Devices → your device → Exposes) and subscribe with `mosquitto_sub -t 'zigbee2mqtt/#' -v`. You should see the state update. If entities remain unavailable, the connection is still failing.

## Rollback Note

If changes break startup, restore your previous `configuration.yaml` from backup and restart. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
