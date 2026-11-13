---
title: 'Zigbee2MQTT Pairing Fails: Coordinator, Permit-Join, Device, Logs'
description: A layered Zigbee2MQTT pairing test that ends with control and state after a restart.
seo_title: Zigbee2MQTT Device Not Pairing? Check the Coordinator
seo_description: A layered Zigbee2MQTT pairing test that ends with control and state after a restart.
keywords:
- zigbee2mqtt pairing failed
- zigbee device not joining
- zigbee2mqtt permit join
date: '2026-11-13'
draft: false
categories:
- Smart Home
category_slug: smart-home
---

<p>Zigbee pairing failures are usually coordinator, permit-join, device reset, or MQTT state. Test one device and read the interview log instead of retrying blindly.</p>
<h2>Before you start</h2><ul>
<li>Zigbee2MQTT with a supported coordinator</li>
<li>One Zigbee device and its reset procedure</li>
<li>Access to the Zigbee2MQTT log and MQTT broker</li>
<li>The device close to the coordinator</li>
</ul>
<h2>Step-by-step checks</h2>
<h3>Step 1: Confirm the coordinator is online</h3>
<p>Open Zigbee2MQTT settings/log and verify the serial adapter is detected with a stable path. Check the coordinator firmware and recent errors.</p>
<p><strong>Check:</strong> The log shows the coordinator started and no serial error is repeating.</p>
<h3>Step 2: Open permit join and watch the log</h3>
<p>Enable permit join for a limited time, then put the device in pairing mode. Follow the interview messages in the log rather than only watching the device list.</p>
<p><strong>Check:</strong> The log shows the device joining or a specific interview error.</p>
<h3>Step 3: Reset the device correctly</h3>
<p>Follow the manufacturer's exact reset/pairing sequence. Keep the device close, remove it from any previous hub, and avoid repeating the reset during the interview.</p>
<p><strong>Check:</strong> The device emits its pairing indication and the interview starts.</p>
<h3>Step 4: Finish the interview and test control</h3>
<p>Wait for the interview to complete, then toggle the device and read its state in Zigbee2MQTT. Check the MQTT topic/entity in Home Assistant.</p>
<p><strong>Check:</strong> Commands work and state updates in the UI.</p>
<h3>Step 5: Restart and repeat</h3>
<p>Restart Zigbee2MQTT, wait for the coordinator, and test the same device again. Confirm it is not marked offline.</p>
<p><strong>Check:</strong> Control and state survive the restart.</p>
<h2>Verify the result</h2>
<p>The device pairs, responds to a control command, reports state, and remains available after a Zigbee2MQTT restart.</p>
<h2>Rollback</h2>
<p>Remove only the test device if pairing is wrong. Keep the coordinator configuration and existing devices unchanged.</p>
<p><a href="/#consult">Ask for help with this exact symptom</a> · <a href="/guides/">All troubleshooting guides</a></p>
