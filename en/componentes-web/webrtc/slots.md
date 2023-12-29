# Slots

Slots are placeholders that contain default elements, but can be replaced with your own elements. For example, to replace the buttons of our `WebRTC` you should add:

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
  <div slot="slot-name">cuxtom content</div>
</videsk-webrtc>
```
{% endcode %}

The available `slots` are:

## Buttons

The list of action buttons such as screen sharing, microphone, camera, hang up, full screen, rotate camera, and chat can be customized or even removed.

* `button-screen`: screen share button
* `button-mic`: microphone button
* `button-cam`: camera button
* `button-hangup`: hang up button
* `button-toggle-camera`: rotate camera button
* `button-chat`: chat button
* `button-fullscreen`: full screen button

<figure><img src="../../.gitbook/assets/image%20(1)%20(1).png" alt=""><figcaption><p>Default available buttons</p></figcaption></figure>

{% hint style="info" %}
The toggle camera and screen share buttons will automatically be displayed if the feature is available on the browser, otherwise they will not be displayed.
{% endhint %}

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
  <button slot="button-screen">Screen share</button>
  <button slot="button-mic">Microphone</button>
  <button slot="button-cam">Camera</button>
  <button slot="button-hangup">Hang up</button>
  <button slot="button-toggle-camera">Rotate camera</button>
  <button slot="button-chat">Chat</button>
  <button slot="button-fullscreen">Full screen</button>
</videsk-webrtc>
```
{% endcode %}

You can use any HTML element inside the `videsk-webrtc` tag, even complex elements like:

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
  <div slot="button-hangup">
    <i class="phone" />
    <span class="tooltip">Hang up</span>
  </div>
</videsk-webrtc>
```
{% endcode %}

## Icons

You can customize the icons:

* `participants-toggle-icons`

```html
<videsk-webrtc>
 <div slot="participants-toggle-icons">
   <!-- Custom icons -->
 </div>
</videsk-webrtc>
```