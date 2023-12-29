---
description: >-
  Here you can find information related to the necessary settings if you have a firewall on the network where Videsk will operate.
---

# ⛔ Firewall

{% hint style="warning" %}
**You only need to apply the following rules to your firewall if your policies are very restrictive or domain-based**. All our traffic is done on ports 80 (UDP/TCP) and 443 (TCP/TLS). If UDP connections are blocked, our system will automatically attempt via TCP.
{% endhint %}

This information will help you correctly configure what is necessary for Videsk to operate in an environment protected by your company's WAFs.

First, you need to understand certain concepts, for that we recommend that you go to the following section.

{% content-ref url="../concepts.md" %}
[concepts.md](../concepts.md)
{% endcontent-ref %}

## 1. NAT Type

The first thing you need to do is determine the type of NAT you have in your business. There are several types of configurations, which will require certain adjustments to allow video calls and other functions to be trafficked:

| NAT Type                      | Description                                                                                                                                                                                                                                                                                                                                      | Requires adjustments   |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| Full-Cone NAT                 | NAT will map the internal IP address and port to a different public IP address and port. Once established, any external host can communicate with the private network host by sending packets to a public IP address and port that has been mapped. This NAT implementation is the least secure, since an attacker can guess which port is open. | ❌                      |
| Restricted Cone NAT           | In the case of the restricted connection, the external IP and port of NAT are open when the host of the private network wants to communicate with a specific IP address outside its network. NAT will block all traffic that does not come from that specific IP address.                                                                        | ✅/❌                    |
| Port-Restricted Cone NAT      | In a port-restricted NAT connection, it will block all traffic unless the private network host has previously sent traffic to a specific IP and port, then only in that case that IP/port will have access to the private network.                                                                                                               | ✅                      |
| Symmetric                     | In this case, the translation of the private IP address to the public IP address depends on the destination IP address where the traffic is to be sent.                                                                                                                                                                                          | ✅                      |

[_Original source_](https://en.wikipedia.org/wiki/Network_address_translation)

## 2. Firewall Type

{% hint style="warning" %}
**You only need to apply the following rules to your firewall if your policies are very restrictive or domain-based**. All our traffic is done on ports 80 (UDP/TCP) and 443 (TCP/TLS). If UDP connections are blocked, our system will automatically attempt via TCP.
{% endhint %}



{% hint style="info" %}
If you have a layer 3 firewall, contact us at [support@videsk.io](mailto:support@videsk.io), with the subject: "**IPs turn servers list"**, to obtain the list of IP addresses of our servers. _We will verify your identity associated with the organization._
{% endhint %}

To add the rules your firewall must allow adding wildcard FQDN lists, that means adding subdomains as follows: `*.videsk.io`

{% hint style="info" %}
You must consider that if the rules applied on the network are on `UDP` and/or `TCP` protocols, at least traffic must be allowed on the `TCP` protocol.
{% endhint %}

## 2. List servers

{% hint style="warning" %}
**You only need to apply the following rules to your firewall if your policies are very restrictive or domain-based**. All our traffic is done on ports 80 (UDP/TCP) and 443 (TCP/TLS). If UDP connections are blocked, our system will automatically attempt via TCP.
{% endhint %}



If you have already recognized the type of NAT and Firewall you have, then proceed to create an access rule to our servers with the following data:

### FQDN

{% hint style="success" %}
We suggest you add our wildcard domain **`*.videsk.io`** to your firewall for maximum compatibility.
{% endhint %}

You must add our `wildcard` TURN servers domain to a white list:

```bash
*.turn.videsk.io
```

{% hint style="danger" %}
We suggest not using IP addresses, as our infrastructure varies depending on the geographical position, so we can increase the number of servers or decrease them according to demand, **we do not recommend using IPs**.
{% endhint %}

{% hint style="info" %}
If you have a layer 3 firewall, contact us at [support@videsk.io](mailto:support@videsk.io), with the subject: "**IPs turn servers list"**, to obtain the list of IP addresses of our servers. _We will verify your identity associated with the organization._
{% endhint %}

For the other applications such as our Rest API, dashboard, console, etc. they are found as top-level subdomains **`*.videsk.io`**. These are:

```bash
app.videsk.io
console.videsk.io
api.videsk.io
assets.videsk.io
cdn.videsk.io
agamotto.videsk.io
exchange.videsk.io
rt.videsk.io
```

In addition to the above domains, we suggest adding the following wildcard domains of third-party services, which allow us to deliver better support.

```
cloudflareinsights.com
*.pendo.io
*.lr-ingest.io
*.ipregistry.co
```

{% hint style="warning" %}
Our services are behind our proxy WAF Cloudflare, the list of servers can be found at the following link: [https://www.cloudflare.com/ips/](https://www.cloudflare.com/ips/)
{% endhint %}

{% hint style="warning" %}
The list of IP addresses of our Sentry error monitor can be found at the following link: [https://docs.sentry.io/product/security/ip-ranges/](https://docs.sentry.io/product/security/ip-ranges/)
{% endhint %}

{% hint style="danger" %}
We use a session monitor called LogRocket, it is currently not possible to list by IP, so we suggest using white lists by base domain.
{% endhint %}

{% hint style="info" %}
**It is important to deliver the best service that our monitoring systems are not blocked by browser extensions, equipment or networks. Otherwise it makes it difficult for our team to proactively identify and resolve issues.**
{% endhint %}

### Ports

{% hint style="warning" %}
**You only need to apply the following rules to your firewall if your policies are very restrictive or domain-based**. All our traffic is done on ports 80 (UDP/TCP) and 443 (TCP/TLS). If UDP connections are blocked, our system will automatically attempt via TCP.
{% endhint %}



We use standard ports such as `80` and `443`, both for communication with our Rest API and our TURN servers.

In the case of our TURN network we use connections through port 80 on `UDP` and `TCP` protocol, which will adapt depending on the `UDP` availability of the network. While port `443` on `TLS/TCP` to use point-to-point encrypted relay if available over the network.

{% hint style="info" %}
In the case of port `80` in all our infrastructure it will automatically redirect to port `443`.
{% endhint %}