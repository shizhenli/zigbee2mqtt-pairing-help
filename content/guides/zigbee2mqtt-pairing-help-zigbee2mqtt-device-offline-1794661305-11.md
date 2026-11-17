---
title: "Zigbee2MQTT Device Offline: Why a Newly Paired Device Stops Reporting State"
description: "A newly paired Zigbee device joins Zigbee2MQTT but stops reporting state shortly after. Check link quality, power, and interview completion to restore reliable reporting."
seo_title: "Zigbee2MQTT Device Offline After Pairing: Fix a Device That Stops Reporting"
seo_description: "A newly paired Zigbee device joins Zigbee2MQTT but stops reporting state shortly after. Check link quality, power, and interview completion to restore reliable reporting."
keywords:
  - "zigbee2mqtt device offline"
date: 2026-11-17T11:13:05+08:00
publishDate: 2026-11-17T11:13:05+08:00
draft: false
categories:
  - "Smart Home"
category_slug: "smart-home"
---

## The scenario

You added a new Zigbee device to Zigbee2MQTT with your USB coordinator, it paired successfully, and then after a short time it stopped reporting state, leaving you with a **zigbee2mqtt device offline** entry in the interface.

## Check the pairing was fully completed

Open the device in the Zigbee2MQTT frontend and look at the interview status. A device that joined but did not finish the interview often behaves exactly like this: it appears once, then goes quiet. If the interview is incomplete, remove the device and pair it again while it sits close to the coordinator. A completed interview should show all expected endpoints and clusters populated.

## Check link quality and power

Look at the link quality value for the device. A low or fluctuating number suggests the device is at the edge of range or behind interference. Move it closer to the coordinator or a known-good router and watch whether reports resume. Also confirm the battery is fresh and seated correctly; a weak cell can carry a device through joining but not through steady reporting.

## Verification test

Trigger the device physically, such as pressing its button or opening the contact, and watch the frontend state update within a few seconds. Then leave it untouched for ten minutes and confirm the last-seen timestamp keeps advancing. If state updates stop again, the device is dropping its link rather than failing to pair.

## Recovery note

If you changed the device location or re-paired it, and behaviour gets worse, remove the device and pair it once more from its final position. Keep a note of the original settings so you can restore them if the new placement does not help.

If the checks above do not explain the drop-off,

![Zigbee2MQTT dashboard showing a paired device and MQTT state](/images/service-detail-960.webp "Zigbee2MQTT device pairing verification")

[Ask for help](/#consult) with your interview status and link quality values.
