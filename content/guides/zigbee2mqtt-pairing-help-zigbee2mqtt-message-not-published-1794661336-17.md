---
title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Failures"
description: "Troubleshoot Zigbee2MQTT when messages are not published to the MQTT broker, causing entities to stay unavailable. Step-by-step checks for USB coordinator and new device setup."
seo_title: "Zigbee2MQTT Message Not Published: Fix MQTT Connection Failures"
seo_description: "Troubleshoot Zigbee2MQTT when messages are not published to the MQTT broker, causing entities to stay unavailable. Step-by-step checks for USB coordinator and new device setup."
keywords:
  - "zigbee2mqtt message not published"
date: 2026-11-18T12:16:59+08:00
publishDate: 2026-11-18T12:16:59+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You've paired a new Zigbee device with your USB coordinator, but Zigbee2MQTT can't publish to the broker and entities remain unavailable.

## Check MQTT Broker Connectivity

First, verify the broker is reachable from the Zigbee2MQTT host. Run `mosquitto_sub -h <broker_ip> -t '#' -v` from the same machine. If you see no output or a connection refused error, the broker is down or blocked. Confirm the broker service is running and that port 1883 (or your configured port) is open. In Zigbee2MQTT's `configuration.yaml`, check the `mqtt` section: `server`, `user`, and `password` must match the broker's credentials exactly. A single typo here causes a **zigbee2mqtt message not published** failure.

## Inspect Zigbee2MQTT Logs

Start Zigbee2MQTT with `DEBUG=*` or check the log output. Look for lines like `MQTT publish failed` or `Connection refused`. If you see `Error: connect ECONNREFUSED`, the broker address is wrong or the broker isn't listening. If you see `Not authorized`, the username or password is incorrect. Correct the credentials in `configuration.yaml` and restart Zigbee2MQTT.

## Verify with a Test Publish

After fixing credentials, publish a test message: `mosquitto_pub -h <broker_ip> -t 'test' -m 'hello'`. Then subscribe to `zigbee2mqtt/#` and trigger a device event (e.g., press a button). You should see a JSON payload. If not, recheck the `base_topic` setting in `configuration.yaml`—it must match the topic you're subscribing to.

## Rollback and Recovery

If changes break things, restore your previous `configuration.yaml` from backup and restart. If the issue persists,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and configuration details.

## Final Check

Ensure the USB coordinator is connected and recognized (`ls /dev/ttyACM*`). A missing coordinator can also prevent publishing. Once broker connectivity and credentials are correct, messages should flow and entities become available.
