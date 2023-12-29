---
description: Discover how to integrate Videsk with other platforms
---

# 🎛 Integrations

If you are here, it's because you are looking to integrate Videsk with other platforms easily and in less than 60 minutes.

The first step is to know in what format and structure the platform will need to receive the data. For this, we suggest searching Google for "_**Platform name**_ Rest API docs".

You can find a list of example integrations in this documentation, but remember that we are compatible with almost all market platforms.

## Playground

Before starting the integration, we recommend using a free platform that allows you to receive requests from our servers to debug and validate that everything is correct before sending real requests to the production service.

| URL                                    | Description                                 | Pricing       |
| -------------------------------------- | ------------------------------------------- | ------------- |
| [Webhook.site](https://webhook.site/)  | Simple, no registration, and fast.          | Free and paid |
| [Request Bin](https://requestbin.com/) | Comprehensive but more complex.             | Free and paid |
| [Ngrok](https://ngrok.com/)            | Local, requires installation and setup.     | Free.         |
| [Cloudflare Tunnel](./#playground)     | Local, requires installation and setup.     | Free.         |

{% hint style="info" %}
We recommend using [webhook.site](./#playground) for integrations. In case you need to develop intermediate servers, we suggest using [ngrok](https://ngrok.com/) or [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation).
{% endhint %}

## Compatibility

**Videsk is only compatible** with platforms that allow receiving **single-shot HTTP requests**, that is, platforms that do not require intermediate steps such as authentication or two-step verification.

For security, all platforms should use at least 1 authorization method via API keys, tokens, passwords, etc., which are sent either in headers, as parameters in the URL, or in few cases in the body of the request. These methods will depend on the platform in question.

{% hint style="warning" %}
It is your responsibility to store tokens, keys, or any type of sensitive information as secrets; otherwise, they could be visible to other people on your team.
{% endhint %}

## Examples of integrations

{% content-ref url="power-bi.md" %}
[power-bi.md](power-bi.md)
{% endcontent-ref %}

{% content-ref url="airtable.md" %}
[airtable.md](airtable.md)
{% endcontent-ref %}
