---
title: "Zigbee2MQTT Coordinator Not Found: Diagnose the USB Adapter Before Pairing"
description: "Zigbee2MQTT cannot open your USB coordinator on startup. Follow these checks to confirm the device path, permissions, and port state before pairing a new Zigbee device."
seo_title: "Zigbee2MQTT Coordinator Not Found: Fix USB Adapter Startup"
seo_description: "Zigbee2MQTT cannot open your USB coordinator on startup. Follow these checks to confirm the device path, permissions, and port state before pairing a new Zigbee device."
keywords:
  - "zigbee2mqtt coordinator not found"
date: 2026-11-17T09:39:36+08:00
publishDate: 2026-11-17T09:39:36+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You started Zigbee2MQTT with a USB coordinator and a new Zigbee device ready to pair, but startup stops at the coordinator is not found step before any controlled diagnosis is done.

## Confirm the coordinator is visible to the host

Unplug the USB coordinator, wait five seconds, then plug it back in. On Linux, run `ls -l /dev/serial/by-id/` and note the exact symlink name. If the directory is empty, the host is not seeing the adapter at all; try another USB port or cable. If a name appears, compare it character by character with the `serial.port` value in your Zigbee2MQTT `configuration.yaml`. A single typo produces the same startup failure.

## Check permissions and port ownership

Run `ls -l` on the resolved device path. The user running Zigbee2MQTT must have read and write access. If it does not, add that user to the `dialout` group, then log out and back in. Also confirm no other process, such as a previous Zigbee2MQTT instance or a serial terminal, is holding the port open. Stop competing services before restarting.

## Verification test

After correcting the path or permissions, restart Zigbee2MQTT and watch the first ten log lines. A healthy start names the adapter and reports the coordinator firmware version. If startup still reports **zigbee2mqtt coordinator not found**, the adapter may be in a bad state: power-cycle it, then retry once.

## Rollback and recovery

If you changed `configuration.yaml`, restore the previous `serial.port` value and restart to return to a known state. Keep a copy of the working configuration before editing again.

If these checks do not resolve it,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and the `by-id` output.
