---
title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found"
description: "Zigbee2MQTT cannot open the USB coordinator on startup? Learn how to check and fix USB adapter permissions so the coordinator is found again."
seo_title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found"
seo_description: "Zigbee2MQTT cannot open the USB coordinator on startup? Learn how to check and fix USB adapter permissions so the coordinator is found again."
keywords:
  - "zigbee2mqtt usb adapter permission"
date: 2026-11-21T17:09:23+08:00
publishDate: 2026-11-21T17:09:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You are running Zigbee2MQTT with a USB coordinator and a new Zigbee device, but at startup Zigbee2MQTT reports that the coordinator is not found, and you need to restore the expected outcome.

## Check the adapter path and permissions

First, confirm the exact device path Zigbee2MQTT is trying to open. Look in your configuration for the serial port setting. Then, on the host, run `ls -l /dev/ttyACM0` (or your adapter's path). The output shows owner and group. If the user running Zigbee2MQTT is not root and not in the group that owns the device, the open will fail. A typical result is `crw-rw---- 1 root dialout`; if your service user is not in `dialout`, that is your cause. Also check that the device node actually exists; if it does not, the adapter may not be plugged in or recognized.

## Fix the permission

Add the service user to the owning group, for example `sudo usermod -aG dialout <user>`. Log out and back in, or restart the service, so the new group membership applies. This is the most common **zigbee2mqtt usb adapter permission** fix. Avoid chmod 777 as a permanent solution; it is insecure and can mask the real issue.

## Verify

Restart Zigbee2MQTT and watch the startup log. A successful open shows the coordinator initializing and the adapter model being detected. If the log still says coordinator not found, recheck the path and group. As a rollback, remove the user from the group with `sudo gpasswd -d <user> dialout` and restore your previous configuration before further changes.

If the error persists after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log output and device path.
