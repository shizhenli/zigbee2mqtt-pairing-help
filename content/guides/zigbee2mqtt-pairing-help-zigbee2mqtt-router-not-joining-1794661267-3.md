---
title: "Zigbee2MQTT Router Not Joining: When the Network Map Stays Empty"
description: "Troubleshoot a Zigbee2MQTT router not joining when the network map shows no coordinator or routers. Step-by-step checks, interpretation, and verification."
seo_title: "Zigbee2MQTT Router Not Joining: Fix an Empty Network Map"
seo_description: "Troubleshoot a Zigbee2MQTT router not joining when the network map shows no coordinator or routers. Step-by-step checks, interpretation, and verification."
keywords:
  - "zigbee2mqtt router not joining"
date: 2026-11-16T08:13:01+08:00
publishDate: 2026-11-16T08:13:01+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

## Troubleshooting

You have a USB coordinator and a new Zigbee router, but Zigbee2MQTT's network map shows neither the coordinator nor any routers, so you cannot confirm the router joined. Start by confirming the map is actually being generated. Open the frontend, go to the Network tab, and click the refresh or scan icon. Wait for the scan to finish. If the map remains blank, the issue is with the coordinator link or the scan, not the new router. Check the Zigbee2MQTT log for lines mentioning the coordinator starting and the network map request. If the log shows the coordinator failed to start, fix that first; a running coordinator is required before any router can appear. Next, verify the router is in pairing mode and close to the coordinator. In the frontend, enable Permit Join for all, then power-cycle the router and watch the log for interview messages. If the log shows nothing, the router is not reaching the network. If it shows an interview starting but never completing, the device is joining but failing the interview. A **zigbee2mqtt router not joining** often comes down to distance or a stale permit join window. Move the router within a few meters of the coordinator, enable Permit Join again, and retry. To verify, refresh the network map: the coordinator should appear, and the router should show as a connected node. If the map is still empty, restart Zigbee2MQTT and repeat the scan once. As a rollback, remove the router from the frontend if it appears as a failed device, then re-add it; this clears partial interview state without touching other devices. If the map stays empty after these checks,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult).
