---
title: "Zigbee2MQTT Coordinator Not Found: Diagnose the USB Adapter Startup Error"
description: "Troubleshoot Zigbee2MQTT when it cannot open the USB coordinator on startup. Check device path, permissions, and port conflicts with step-by-step verification."
seo_title: "Fix zigbee2mqtt coordinator not found: USB adapter startup error"
seo_description: "Troubleshoot Zigbee2MQTT when it cannot open the USB coordinator on startup. Check device path, permissions, and port conflicts with step-by-step verification."
keywords:
  - "zigbee2mqtt coordinator not found"
date: 2026-11-28T22:04:35+08:00
publishDate: 2026-11-28T22:04:35+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You start Zigbee2MQTT with a USB coordinator and a new Zigbee device waiting to pair, but the log stops at the coordinator is not found step and you cannot complete a controlled diagnosis.

## Confirm the adapter path and permissions

Open your Zigbee2MQTT configuration and find the serial port setting. On Linux it often looks like `/dev/ttyACM0` or `/dev/ttyUSB0`. Run `ls -l /dev/serial/by-id/` and compare the stable by-id path to the configured value. If the configured path is missing, update it to the by-id entry. Next, check permissions: run `ls -l` on the device node. If your Zigbee2MQTT user is not in the `dialout` group, add it and restart the service. A permission error usually appears as "Permission denied" rather than "No such file".

## Rule out port conflicts and power

Stop any other service that may hold the adapter, such as another Zigbee stack or a serial terminal. Unplug the coordinator, wait five seconds, and reconnect it directly to the host, not through an unpowered hub. Then start Zigbee2MQTT again and read the first error line. If it says the device is busy, a process still owns the port. If it says the device cannot be opened, the path or permissions are still wrong.

## Verification test

With the corrected path and group membership, restart Zigbee2MQTT and watch the startup log. A healthy start shows the coordinator firmware and IEEE address, then the network comes online. If you still see the **zigbee2mqtt coordinator not found** message, capture the full log from the first error and confirm the adapter is visible in `dmesg` after reconnecting.

## Rollback and recovery

If changes make things worse, restore your previous configuration file and re-add the original serial path. Keep a backup before editing. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
