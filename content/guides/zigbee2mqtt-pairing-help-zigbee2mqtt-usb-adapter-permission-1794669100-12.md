---
title: "USB Coordinator Permission Denied: Restoring Zigbee2MQTT Startup"
description: "Zigbee2MQTT cannot open your USB coordinator on startup? Learn how to check permissions, verify access, and recover safely when the coordinator is not found."
seo_title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found"
seo_description: "Zigbee2MQTT cannot open your USB coordinator on startup? Learn how to check permissions, verify access, and recover safely when the coordinator is not found."
keywords:
  - "zigbee2mqtt usb adapter permission"
date: 2026-11-25T10:13:24+08:00
publishDate: 2026-11-25T10:13:24+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and a new Zigbee device, but startup stops at the coordinator is not found step because the adapter cannot be opened.

## Check the device path and ownership

First, confirm the coordinator's device path. On Linux, run `ls -l /dev/serial/by-id/` and note the full path for your adapter. Then check ownership with `ls -l /dev/ttyACM0` (or the path you found). The user running Zigbee2MQTT must have read and write access. If the device is owned by root and group dialout, add your user to dialout: `sudo usermod -aG dialout $USER`. Log out and back in for the change to take effect. This is the most common **zigbee2mqtt usb adapter permission** issue.

## Interpret the result

If `ls -l` shows your user or a group you belong to with rw access, permissions are correct. If not, fix them as above. Also check that the path in your Zigbee2MQTT configuration matches the by-id path exactly; a mismatch causes the same symptom.

## Verification test

After adjusting permissions, restart Zigbee2MQTT and watch the log. A successful start shows the coordinator opening without a permission error. You can also test manually: `sudo -u <zigbee2mqtt-user> test -r /dev/ttyACM0 && echo readable`. If that prints readable, the user has access.

## Rollback and recovery

If the coordinator still fails, revert any recent permission changes and try the original path. Keep a note of the working configuration before further edits. If the adapter is not detected at all, check the USB cable and port.

If these steps do not restore startup,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log output and device path.
