---
description: >-
  Below you will find some important concepts to consider
  before integrating Videsk into your website.
---

# 💆♀ Headers

Depending on the configuration of your website and where it is hosted you will need to configure certain headers on your web server.

{% hint style="info" %}
**Headers are optional**, but they are suggested to add more security to your website. **If you don't have any of them it is not mandatory to add them.**
{% endhint %}

## Feature-Policy or Permissions-Policy

This header defines where and what types of browser features can be used on your site, such as camera, microphone, GPS, gyroscope, battery, etc. If you have this header enabled, you should add the following to the list:

```
Feature-Policy: microphone 'self'; camera 'self'; autoplay 'self'; ...
Permissions-Policy: autoplay=(self), camera=(self), fullscreen=(self), microphone=(self), picture-in-picture=(self)
```

## X-Frame-Options

This header is vital in terms of security, it prevents your website from being embedded in an external one, impersonating your identity and potentially extracting data from your users. Therefore, we suggest you add it at least in `SAMEORIGIN`.

```
X-Frame-Options: SAMEORIGIN;
```

{% hint style="info" %}
If you set the value to `DENY` you could lose some Videsk functionalities.
{% endhint %}

## Content-Security-Policy

This header (CSP) allows you to define what type of content is allowed to be loaded for each service and type of resource registered in this header.

```
Content-Security-Policy: script-src *.videsk.io; style-src *.videsk.io; prefetch-src *.videsk.io; media-src *.videsk.io; ....
```

## Content-Security-Policy-Report-Only

This header allows you to experiment with certain header policies before officially implementing them, without necessarily generating a real impact on your site, thus giving you the option to monitor behavior.

We suggest you add the same as in Content-Security-Policy (CSP).