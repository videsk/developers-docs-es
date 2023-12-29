---
description: Let us explain why it's mandatory to have a valid SSL on your website.
---

# 🔐 SSL

**Secure Sockets Layer** is an important protocol for enhancing data security and authentication on the Internet. It has been a hot topic due to movements like [Encrypt All The Things](https://encryptallthethings.net/) and Google's push for wider SSL adoption.

In addition to the above, there are certain technologies, such as those used by Videsk, that require a valid SSL to ensure the security of data transmission between your customers and your team.

## Why do I need one?

Videsk uses real-time technology, one of which is WebRTC, which requires secure connections through your SSL certificate, ensuring that the connection between your customer and someone on your team is 100% encrypted, preventing data leaks of video, audio, chat, files, etc.

{% hint style="warning" %}
Remember, it is **not optional** to have an SSL certificate.
{% endhint %}

## What happens if my SSL expires?

This is a serious problem, as most of your customers will not be able to access your website due to a browser message indicating this issue.

We suggest you purchase a new one, either paid or free, as soon as possible.

{% hint style="info" %}
Whether to choose a paid or free certificate will depend on the needs and characteristics of your business. Most websites only require a free certificate.
{% endhint %}

## Is it compatible with wildcard SSL, multi-domain, EV, etc.?

Yes. The only relevant thing is that the SSL is valid for the domain where it is installed, that it is current, and that you make sure it has been issued correctly by a recognized provider.

## Can I test locally or on localhost without SSL?

Yes, but you will need to use your local IP or `127.0.0.1` since `localhost` is reserved for local testing by our development team. Also, depending on your browser, you will need to force `https://` at the beginning of the URL and then click Advanced and continue.