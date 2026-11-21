---
title: "Zigbee2MQTT Coordinator Not Found: Resolve the USB Adapter Startup Error"
description: "Troubleshoot Zigbee2MQTT coordinator not found when the USB adapter fails to open on startup. Step-by-step checks, verification, and recovery."
seo_title: "Fix Zigbee2MQTT Coordinator Not Found: USB Adapter Startup Error"
seo_description: "Troubleshoot Zigbee2MQTT coordinator not found when the USB adapter fails to open on startup. Step-by-step checks, verification, and recovery."
keywords:
  - "zigbee2mqtt coordinator not found"
date: 2026-11-21T17:06:21+08:00
publishDate: 2026-11-21T17:06:21+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and a new Zigbee device, but startup halts at the coordinator is not found step before any diagnosis completes.

## Confirm the Error and Check the Basics

First, look at the Zigbee2MQTT log. The exact message usually reads "Error: Coordinator not found" or "Failed to open serial port." This means Zigbee2MQTT cannot open the USB coordinator. Do not proceed until you see that line.

Next, verify the USB coordinator is physically connected and powered. Try a different USB port, preferably a USB 2.0 port directly on the computer, not a hub. Then check the device path in your configuration.yaml under serial: port. On Linux, run ls -l /dev/serial/by-id/ and confirm the coordinator's ID matches the configured path. On Windows, check Device Manager for the COM port number. If the path is wrong or missing, correct it and restart Zigbee2MQTT.

## Test Permissions and Driver

On Linux, ensure your user is in the dialout group: groups $USER. If not, add it with sudo usermod -a -G dialout $USER and log out and back in. Also confirm the correct driver is loaded (cp210x or ch341) using dmesg | grep tty. If the adapter appears but Zigbee2MQTT still reports **zigbee2mqtt coordinator not found**, try a different USB cable. A charge-only cable will not work.

## Verification Test

After fixing the path or permissions, restart Zigbee2MQTT and watch the log. Success looks like "Coordinator firmware version" and "Zigbee2MQTT started." If the error persists, stop and do not attempt further changes.

## Rollback and Recovery

If you edited configuration.yaml, revert to the previous working serial port path and restart. Keep a backup of your configuration before changes. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt and adapter model.
