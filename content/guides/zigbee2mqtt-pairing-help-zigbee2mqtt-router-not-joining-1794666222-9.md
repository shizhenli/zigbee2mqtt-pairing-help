---
title: "Zigbee2MQTT Router Not Joining: When the Network Map Shows No Coordinator or Routers"
description: "Troubleshoot a Zigbee2MQTT router not joining when the network map shows no coordinator or routers. Step-by-step checks, result interpretation, and a verification test."
seo_title: "Zigbee2MQTT Router Not Joining: Fix an Empty Network Map"
seo_description: "Troubleshoot a Zigbee2MQTT router not joining when the network map shows no coordinator or routers. Step-by-step checks, result interpretation, and a verification test."
keywords:
  - "zigbee2mqtt router not joining"
date: 2026-11-21T17:12:23+08:00
publishDate: 2026-11-21T17:12:23+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

You have a USB coordinator and a new Zigbee device, but when you open the network map it is completely empty—no coordinator, no routers—so you cannot confirm whether your **zigbee2mqtt router not joining** issue is a device problem or a network problem.

## Check the coordinator link first

Open the Zigbee2MQTT web interface and look at the top status bar. If it shows a red or disconnected state, the map cannot populate. Confirm the USB coordinator is listed under Settings > Serial with the correct port (for example, /dev/ttyACM0 or /dev/ttyUSB0). A wrong port or missing permission produces an empty map every time. After correcting it, restart Zigbee2MQTT and wait 60 seconds before reopening the map.

## Confirm the map is actually generating

Go to the Network Map tab and click the refresh/update button. If the page stays blank with no nodes at all, check the Zigbee2MQTT log for lines containing "network map" or "requesting". A timeout or "not supported" message means the coordinator firmware does not answer map requests; update the coordinator firmware, then retry. If the log shows a successful response but the page is still empty, clear the browser cache and reload.

## Verification test

With the coordinator connected, power on one known-working router that is already joined. Refresh the map. The coordinator and that router should now appear as connected nodes. If they do, the map is healthy and your new device is the remaining variable; if they do not, the coordinator link is still the fault.

## Rollback note

If a firmware or serial-port change caused the empty map, restore the previous coordinator firmware and port setting, restart, and confirm the map returns before changing anything else. For guided diagnosis,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
