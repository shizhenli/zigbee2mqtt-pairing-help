---
title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found on Startup"
description: "Zigbee2MQTT cannot open your USB coordinator at startup? Fix zigbee2mqtt usb adapter permission issues with clear checks, a verification test, and a safe rollback."
seo_title: "Zigbee2MQTT USB Adapter Permission: Fix Coordinator Not Found"
seo_description: "Zigbee2MQTT cannot open your USB coordinator at startup? Fix zigbee2mqtt usb adapter permission issues with clear checks, a verification test, and a safe rollback."
keywords:
  - "zigbee2mqtt usb adapter permission"
date: 2026-11-15T19:23:48+08:00
publishDate: 2026-11-15T19:23:48+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You start Zigbee2MQTT with a new device waiting to pair, but startup stops at "coordinator is not found" because the USB adapter cannot be opened.

## Confirm the permission error

Stop Zigbee2MQTT, then check the adapter path in configuration.yaml. Run `ls -l /dev/ttyUSB0` (or your actual path, such as /dev/ttyACM0) and note the owner and group. If the device shows root:dialout and your Zigbee2MQTT user is not in dialout, that is your failure. Also run `groups zigbee2mqtt` (replace with your service user) and confirm dialout appears. If it does not, add the user: `sudo usermod -aG dialout zigbee2mqtt`. Log out and back in, or restart the service, so the new group membership applies. This is the most common **zigbee2mqtt usb adapter permission** problem.

## Rule out the wrong device

Unplug the coordinator and run `ls /dev/ttyUSB* /dev/ttyACM*` again. If the path disappears and returns with a different name, update configuration.yaml to match. If two adapters are present, verify the serial number in the logs rather than guessing. A path that changes after reboot will reproduce the same startup error even when permissions are correct.

## Verification test

Restart Zigbee2MQTT and watch the first lines of the log. Success means the coordinator opens and the startup message no longer reports "coordinator is not found"; the expected outcome is that the coordinator is found and the service proceeds to permit join. If the same error remains, check `dmesg | tail` for USB disconnect messages and confirm the adapter is seated in a powered port.

## Rollback and recovery

If you changed group membership or the device path, revert configuration.yaml to the previous path and remove the user from dialout with `sudo gpasswd -d zigbee2mqtt dialout`, then restart. Keep a copy of the working configuration before editing. For a controlled diagnosis of your specific setup,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
