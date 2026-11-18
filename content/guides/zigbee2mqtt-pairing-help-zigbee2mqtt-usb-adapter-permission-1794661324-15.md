---
title: "Zigbee2MQTT USB Adapter Permission: Fix 'Coordinator Not Found' on Startup"
description: "Troubleshoot Zigbee2MQTT USB adapter permission errors that cause 'coordinator not found' on startup. Step-by-step checks and verification."
seo_title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found"
seo_description: "Troubleshoot Zigbee2MQTT USB adapter permission errors that cause 'coordinator not found' on startup. Step-by-step checks and verification."
keywords:
  - "zigbee2mqtt usb adapter permission"
date: 2026-11-18T10:48:55+08:00
publishDate: 2026-11-18T10:48:55+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You're setting up Zigbee2MQTT with a USB coordinator and a new Zigbee device, but at the 'coordinator is not found' step, Zigbee2MQTT cannot open the USB coordinator on startup.

## Check the device path and permissions

First, confirm the adapter's device path. Run `ls -l /dev/serial/by-id/` and note the symlink for your coordinator. Then check its permissions with `ls -l /dev/ttyACM0` (or the actual device). The output should show the owner and group, typically `root dialout`. If your Zigbee2MQTT user is not in the `dialout` group, it lacks access. Add the user: `sudo usermod -aG dialout yourusername`, then log out and back in. This is the most common **zigbee2mqtt usb adapter permission** issue.

## Verify the configuration

In your Zigbee2MQTT `configuration.yaml`, ensure `serial.port` points to the stable `/dev/serial/by-id/...` path, not a volatile `/dev/ttyUSB0`. A wrong path yields the same 'coordinator not found' error. Also check that no other process (like ModemManager) is holding the port: `sudo lsof /dev/ttyACM0`. If ModemManager is present, disable it or add a udev rule to ignore the device.

## Verification test

After fixing permissions and configuration, restart Zigbee2MQTT. Watch the logs: you should see 'Coordinator firmware version' and 'Zigbee2MQTT started'. If the error persists, test access directly: `sudo -u zigbee2mqtt cat /dev/ttyACM0` (adjust user). A 'Permission denied' confirms the group issue; no output means access is granted.

## Rollback and recovery

If changes cause new problems, revert the group membership with `sudo gpasswd -d yourusername dialout` and restore your previous `configuration.yaml`. Keep a backup before editing. For persistent issues,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your logs and `ls -l` output.

Once permissions are correct, Zigbee2MQTT will open the coordinator and proceed to pairing your new device.
