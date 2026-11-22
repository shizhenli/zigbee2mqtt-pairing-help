---
title: "Zigbee2MQTT Can't Open Your USB Coordinator: A Startup Fix"
description: "Zigbee2MQTT cannot open your USB coordinator on startup? Follow these checks to diagnose the port, permissions, and adapter path, then verify pairing works again."
seo_title: "Zigbee2MQTT Coordinator Not Found: USB Startup Fix"
seo_description: "Zigbee2MQTT cannot open your USB coordinator on startup? Follow these checks to diagnose the port, permissions, and adapter path, then verify pairing works again."
keywords:
  - "zigbee2mqtt coordinator not found"
date: 2026-11-22T09:13:27+08:00
publishDate: 2026-11-22T09:13:27+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and a new Zigbee device, but startup stops at the coordinator is not found step before you can run a controlled diagnosis.

## Confirm the coordinator is actually present

Unplug and replug the USB coordinator, then run `ls -l /dev/serial/by-id/`. You should see a stable entry like `usb-ITead_Sonoff_Zigbee_3.0_USB_Dongle_Plus...`. If the directory is empty, the host is not seeing the adapter: try another USB port or cable. If an entry appears, copy its full path; this is the value Zigbee2MQTT needs.

## Check the configured port and permissions

Open your Zigbee2MQTT `configuration.yaml` and inspect `serial.port`. It must match the by-id path exactly, including case. A common cause of **zigbee2mqtt coordinator not found** is a stale `/dev/ttyUSB0` entry that changed after a reboot. Also confirm your user is in the `dialout` group (`groups`) and that the device node is readable (`ls -l` on the path). Fix permissions with `sudo usermod -aG dialout $USER`, then log out and back in.

## Verification test

Stop Zigbee2MQTT, start it in the foreground, and watch the log. A healthy start prints the adapter type and firmware version, then "Coordinator firmware version". If you still see the coordinator error, the port path or permissions are wrong. Once startup is clean, enable permit join and confirm your new device appears.

## Rollback note

If a recent configuration edit caused this, restore your previous `configuration.yaml` from backup before changing permissions further. Keep a copy of the working by-id path so future reboots do not break startup. If the adapter remains invisible to the host, the hardware or cable may need replacement.

For a guided review of your logs and configuration,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
