---
title: "Zigbee2MQTT Device Not Pairing: Check the Coordinator First"
description: "A practical first-pass check for Zigbee2MQTT Pairing Help."
date: 2026-11-13
---
<p>Pairing failures are often coordinator, channel, or device-mode issues. I test one device and one command path.</p>
<h2>1. Reproduce the exact failure</h2>
<p>Write down what works, what does not, and the last change. Test from the same device and network where the problem happens. A second device is useful only as a comparison, not as proof.</p>
<h2>2. Check the layer before the app</h2>
<p>Confirm the host is reachable, the account or device is allowed, and the local client can see the service. Then test the app setting. Changing three layers at once makes the result impossible to interpret.</p>
<h2>3. Make one change and retest</h2>
<p>Record the old value, apply one change, retest, and keep the result. If the change does not fix it, roll it back before trying the next path.</p>
<h2>4. Handover test</h2>
<p>Repeat the successful test after a restart or reconnect. A fix that only works in the current session is not ready for handover.</p>
<p><a href="/">Back to the service page</a> · <a href="mailto:hello@handytasklab.com?subject=Zigbee2MQTT%20Pairing%20Help%20question&body=Source%3A%20zigbee2mqtt-pairing-help">Ask about this exact symptom</a></p>
