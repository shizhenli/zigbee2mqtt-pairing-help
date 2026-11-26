---
title: "Zigbee2MQTT Permit Join Never Finds a Device: A Controlled Diagnosis"
description: "Permit join runs but your new Zigbee device never appears in Zigbee2MQTT? Follow this controlled diagnosis to isolate the cause and restore pairing."
seo_title: "Zigbee2MQTT Permit Join Never Finds a Device: Fix It Step by Step"
seo_description: "Permit join runs but your new Zigbee device never appears in Zigbee2MQTT? Follow this controlled diagnosis to isolate the cause and restore pairing."
keywords:
  - "zigbee2mqtt permit join"
date: 2026-11-26T09:11:42+08:00
publishDate: 2026-11-26T09:11:42+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have started permit join in Zigbee2MQTT with your USB coordinator, but the new Zigbee device never appears in the interface. Before changing settings randomly, run this controlled diagnosis to find where the join process is breaking.

## Confirm permit join is actually active

Open the Zigbee2MQTT frontend and check the permit join status. It should show a countdown (usually 254 seconds). If it shows 0 or is disabled, enable it again and watch the log. A healthy log shows `Permit join enabled` and later `Zigbee: allowing new devices to join`. If you see no such line, the command is not reaching the coordinator.

## Check the coordinator link

In the log, look for errors such as `Coordinator failed to start` or repeated `requestQueue` timeouts. Unplug the USB coordinator, wait ten seconds, and reconnect it. Then restart Zigbee2MQTT. If the log now shows the coordinator firmware and channel, the link is healthy. If not, try a different USB port or a powered hub; USB 3.0 ports can cause interference.

## Test with a known-good device

Bring a device that paired before within one metre of the coordinator and start **zigbee2mqtt permit join** again. If it appears, the coordinator and network are fine, and the new device is the problem: reset it fully and check its battery. If the known-good device also fails, the issue is on the coordinator side.

## Verify and recover

After any change, repeat the join and confirm the device appears with a model name in the frontend. If you altered channel or pan ID during diagnosis, restore the previous values and restart before re-pairing existing devices. If the device still never appears,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your log excerpt.
