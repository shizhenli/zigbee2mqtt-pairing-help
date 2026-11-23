---
title: "Zigbee2MQTT Message Not Published: Fix Broker Publishing When Connection Fails"
description: "Troubleshoot Zigbee2MQTT when it cannot publish to the MQTT broker, leaving entities unavailable. Step-by-step checks for USB coordinator and new device setup."
seo_title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Fails"
seo_description: "Troubleshoot Zigbee2MQTT when it cannot publish to the MQTT broker, leaving entities unavailable. Step-by-step checks for USB coordinator and new device setup."
keywords:
  - "zigbee2mqtt message not published"
date: 2026-11-23T10:13:33+08:00
publishDate: 2026-11-23T10:13:33+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've added a new Zigbee device and your Zigbee2MQTT logs show a connection failure to the MQTT broker, so entities remain unavailable and you see the **zigbee2mqtt message not published** error before any controlled diagnosis.

## Check the Broker Connection Settings

Open your Zigbee2MQTT configuration (usually `configuration.yaml`) and verify the `mqtt` section. Confirm the `server` URL matches your broker's address and port (e.g., `mqtt://192.168.1.10:1883`). Check `user` and `password` if your broker requires authentication. A common mistake is using `localhost` when Zigbee2MQTT runs in a container—use the host IP or service name instead. After saving, restart Zigbee2MQTT and watch the logs. If you see `MQTT connect error` or `Connection refused`, the broker is unreachable or credentials are wrong.

## Verify Broker Reachability

From the same machine running Zigbee2MQTT, test the broker with a simple command: `mosquitto_sub -h <broker-ip> -p 1883 -t '#' -v`. If it connects, the broker is fine and the issue is in Zigbee2MQTT's config. If it fails, check firewall rules, broker service status, and network routing. Also ensure the USB coordinator is recognized—run `ls /dev/ttyACM*` or `ls /dev/ttyUSB*` and confirm the path in `serial.port` matches. A missing coordinator can cause Zigbee2MQTT to start but fail to publish.

## Verification Test

After fixing the config, restart Zigbee2MQTT and check the log for `Connected to MQTT server`. Then publish a test message from the Zigbee2MQTT frontend (e.g., toggle a light) and subscribe with `mosquitto_sub -t 'zigbee2mqtt/#' -v`. You should see the state change. If entities remain unavailable, recheck the `base_topic` setting—it must match your subscription.

## Rollback and Recovery

If changes break startup, revert to your previous `configuration.yaml` backup and restart. Keep a known-good config to restore quickly. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and config details.
