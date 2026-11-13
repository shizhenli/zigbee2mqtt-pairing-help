---
title: Zigbee2MQTT Pairing Help
seo_title: Zigbee2MQTT Pairing Help | Device Not Joining
seo_description: Remote help for Zigbee2MQTT pairing failures, coordinator state, permit-join, and MQTT verification.
keywords:
- zigbee2mqtt pairing failed
- zigbee device not joining
- zigbee2mqtt permit join
hero_kicker: ZIGBEE2MQTT AND HOME ASSISTANT
hero_h1: Zigbee device refuses to pair?
hero_lead: Separate coordinator, permit-join, device mode, and MQTT state, then verify control and a restart before adding more devices.
hero_proof:
- One coordinator and one device
- Permit-join and device mode checked
- Control, state, and restart verified
hero_alt: A monitor and small Zigbee coordinator on a wooden desk
hero_title: Zigbee2MQTT coordinator and dashboard
body_alt: Zigbee2MQTT dashboard showing a paired device and MQTT state
body_title: Zigbee2MQTT device pairing verification
body_caption: A paired interview is not enough; control and state must survive a restart.
failures_kicker: THE THREE FAILURES WE SEE
failures_heading: What is going wrong?
test_kicker: HOW WE TEST
test_heading: Find the failing layer, then prove the fix.
scope_kicker: SERVICE SCOPE
scope_heading: What is included
scope_note: The session covers one agreed device and one verified path. Anything outside the written scope is quoted separately before work starts.
faq_kicker: FAQ
faq_heading: Before you book
consult_heading: Tell us what is happening.
consult_lead: Send the device, software, exact symptom, and what you have already tried. We will confirm scope and a fixed quote before booking.
form_placeholder: Device, software version, exact symptom, and what you have tried.
first_guide_url: /guides/zigbee2mqtt-pairing-help/
symptoms:
- title: Permit join never finds it
  text: Zigbee2MQTT is in permit-join mode, but the device never appears in the interview list.
- title: Interview starts then fails
  text: The device appears briefly, then the interview stalls or the device is marked unsupported.
- title: Paired but uncontrollable
  text: The device is in the list, but state updates or commands do not reach it.
checks:
- title: Confirm the coordinator
  text: Check the adapter is detected, the serial path is stable, and the coordinator firmware is supported. A coordinator offline explains every pairing failure.
- title: Enable permit join
  text: Allow join for the intended duration and keep the device close during the interview. Check the Zigbee2MQTT log, not only the dashboard.
- title: Reset the device correctly
  text: Use the manufacturer's pairing/reset sequence; holding a button for the wrong duration can factory-reset or do nothing.
- title: Verify control after restart
  text: Toggle the device, read its state, then restart Zigbee2MQTT and repeat.
included:
- One coordinator and one Zigbee device
- Coordinator/serial and permit-join checks
- Device reset and interview review
- Control and restart verification
excluded:
- Electrical wiring or mains installation
- Buying new hardware
- Custom converter development
- Guaranteeing every end device
faqs:
- q: Should I pair all devices at once?
  a: No. Pair one known device first so the coordinator, permit-join, and MQTT path are proven before adding more.
- q: Why does the device disappear after a restart?
  a: The interview may not have completed, or the device is not reaching the coordinator. Check the log and the network path.
- q: Can you fix faulty hardware?
  a: No. We isolate coordinator, pairing, and MQTT issues; physical repair or wiring is outside scope.
---
