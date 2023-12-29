---
description: >-
  You will find concepts related to technology, networks and connections we use.
---

# ☝ Concepts

## WebRTC

WebRTC is the technology that powers seamless end-to-end secure connections between browsers based on DTLS-SRTP protocols. **This means you do not need to install extensions or plugins in your device to have a secure connection.**

Although it can be used for various purposes, at Videsk we use it as our highspeed connection medium for most of our features.

## P2P (Peer-to-Peer)

P2P is a peer-to-peer connection model capable of connecting networks directly without using servers or proxies as intermediaries. This technology has been used for years, and is more commonly known in file downloads such as torrents.

The great benefits of this type of connection are its fast and scalable data transfer speeds, although it also has restrictions when used with certain restrictive WAF protected networks, due to requiring an open type of NAT for autodetection of a user's public/LAN IP and ports.

In certain cases it is not possible to execute P2P connections, so it is necessary to use a relay server to distribute the data.

## Relay Server

A relay server or TURN server, allows you to connect in environments where you have restrictive networks such as symmetric NATs that restrict IP addresses and/or ports.

They are also used in certain cases when the connection is not stable and requires a single access point to transmit video and audio data.&#x20;

This type of connection using relay servers adds some latency because it requires accessing our servers that participate as a relay between the video call participants.