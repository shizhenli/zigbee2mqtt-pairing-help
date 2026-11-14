---
title: "Zigbee2MQTT Coordinator Not Found: Fix the USB Adapter Startup Error"
description: "Zigbee2MQTT cannot open your USB coordinator on startup? Follow these checks to confirm the port, permissions, and adapter path, then verify and recover safely."
seo_title: "Zigbee2MQTT Coordinator Not Found: USB Adapter Fix"
seo_description: "Zigbee2MQTT cannot open your USB coordinator on startup? Follow these checks to confirm the port, permissions, and adapter path, then verify and recover safely."
keywords:
  - "zigbee2mqtt coordinator not found"
date: 2026-11-14T20:04:28+08:00
publishDate: 2026-11-14T20:04:28+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You started Zigbee2MQTT with a USB coordinator and a new Zigbee device to pair, but startup stops at the coordinator step with a not-found error.

## Confirm the coordinator is visible to the host

Unplug and replug the USB coordinator, then list serial devices on the host. On Linux, run `ls -l /dev/serial/by-id/`. You should see an entry containing the adapter's vendor name, such as `usb-ITead_Sonoff_Zigbee_3.0_USB_Dongle_Plus...`. If the directory is empty or the entry disappears after replugging, the problem is physical: try another USB port, a powered hub, or a different cable. A missing by-id entry means Zigbee2MQTT has nothing to open.

## Check the configured port and permissions

Open your Zigbee2MQTT `configuration.yaml` and inspect the `serial` section. The `port` value must match the by-id path exactly, including case. Avoid `/dev/ttyUSB0` because it can change between reboots. Then confirm your user is in the `dialout` group on Linux; run `groups` and look for `dialout`. If it is absent, add the user and log out and back in. A permission denial often surfaces as a generic open failure.

## Verification test

Stop Zigbee2MQTT, then run a direct read test: `cat /dev/serial/by-id/<your-adapter>`. It will emit binary noise; press Ctrl+C. If the command returns permission denied or no such file, the coordinator is still not reachable. Restart Zigbee2MQTT and watch the log. A healthy start shows the adapter opening and the coordinator firmware version. If it still reports **zigbee2mqtt coordinator not found**, the path or device is still wrong.

## Rollback and recovery

Before editing, copy `configuration.yaml` to `configuration.yaml.bak`. If a change makes startup worse, restore the backup and replug the adapter. If the by-id entry never appears on any port, the adapter may have failed; test it on another host before replacing it. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
