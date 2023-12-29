---
description: >-
  Here you'll see how to get the most out of our WebRTC as a web component.
---

# 📹 WebRTC

A web component allows our `WebRTC` to operate as a native DOM element of the browsers. In this way, you can interact with it as with an HTML tag.

Within our `WebRTC` you can customize the available buttons, add custom elements, change the layout, listen to events, define your own CSS and much more.

Our web component aims to provide a unique flexibility when it comes to customizing your customers' experiences.

To be able to customize our `WebRTC` as a web component, you must define the tag in some part of your HTML code:

{% code lineNumbers="true" %}
```html
<videsk-webrtc></videsk-webrtc>
```
{% endcode %}

{% hint style="info" %}
If you define the web component, remember to [reference it in our SDK](../../sdks/webrtc/methods.md#create), otherwise a new one will be created.
{% endhint %}

You can use our web component independently of our SDK, but you will have to take charge of the `WebSocket` connections with our signaling server `wss://exchange.videsk.io`.