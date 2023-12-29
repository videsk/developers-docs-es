---
description: >-
  Learn how to perform diagnostics on your team and/or network when video calls do not connect in corporate environments.
---

# WebRTC

## Tests

This documentation aims to help you identify problems related to a device or the network.

{% hint style="warning" %}
Remember to perform these tests on the device where you are experiencing issues. If the issues are network-related, you can use any device, but it must be connected to the same network.
{% endhint %}

1. Access this [link](https://gauge.videsk.io/)
2. Click on the green `Start` button
3. Wait for the tests to finish with "Video Bandwidth" completed
4. At the top, look for the "bug" icon to the left of the green `Start` button.
5. Then click on `Download report`
6. Send us an email at [support@videsk.io](mailto:support@videsk.io), with the subject "WebRTC Tests" indicating the name of your company, attaching the file `testrtc-...Z.log`

## Reasons for Issues

Read on to understand why your agents might not be connecting correctly.

### Peripherals

{% hint style="info" %}
The tests may report errors in the microphone if it is turned off or muted from your device or keyboard.
{% endhint %}

![Error capturing audio](<../.gitbook/assets/image (60).png>)

As a minimum requirement, you must have a microphone to join video calls.

![Successfully detecting camera](<../.gitbook/assets/image (33).png>)

### Network

To identify network problems, it is necessary to understand certain concepts.

![Network tests](<../.gitbook/assets/image (51).png>)

`Network` consists of network-specific tests, requiring at least `UDP` or `TCP` connections. If both types of transmission protocols are restricted, you will not be able to connect to video calls.

{% hint style="info" %}
IPv6 compatibility is not required.
{% endhint %}

![Connectivity tests](<../.gitbook/assets/image (59).png>)

For `Connectivity`, these are the connection tests, where the availability to connect from your network with `Relay`, i.e., relay servers, `Reflexive` for P2P connection outside the network, and finally `Host` connection also P2P but within the network, will be tested.

Depending on your network policies and use case, you should have at least one type of connection available. In cases where your clients or agents are outside your network, you need at least `Relay` availability.

We suggest reading our Firewall configuration documentation.

{% content-ref url="../seguridad/firewall.md" %}
[firewall.md](../seguridad/firewall.md)
{% endcontent-ref %}

If your clients and agents (both) are within the same network, you must have a `Host` connection.
