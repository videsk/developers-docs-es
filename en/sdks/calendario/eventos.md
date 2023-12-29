---
description: >-
  We explain how events work and what to do when they are triggered.
---

# Events

## `days`

This event is triggered when the `getDays` method has been called. The event contains the same return values as the `getDays` method.

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('days', event => {
    const days = event.detail;
});
[REPLACE_CODE_FORMAT]

## `hours`

This event is triggered when the `getHours` method has been called. The event contains the same return values as the `getHours` method.

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('hours', event => {
    const hours = event.detail;
});
[REPLACE_CODE_FORMAT]

## `created`

This event is triggered when the `create` method has been called. The event contains the same return values as the `create` method.

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('created', event => {
    const response = event.detail;
});
[REPLACE_CODE_FORMAT]

## `canceled`

This event is triggered when the `cancel` method has been called. The event contains the same return values as the `cancel` method.

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('canceled', event => {
    const response = event.detail;
});
[REPLACE_CODE_FORMAT]

## `rescheduled`

This event is triggered when the `reschedule` method has been called. The event contains the same return values as the `reschedule` method.

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('rescheduled', event => {
    const response = event.detail;
});
[REPLACE_CODE_FORMAT]

## `join`

This event is triggered when the `join` method has been called. The event contains the `accessToken` needed to start the video call.

{% hint style="info" %}
With this event, you should use our [WebRTC](../webrtc/#use) SDK.
{% endhint %}

{% hint style="danger" %}
Remember to listen for the [hangup](../webrtc/metodos.md#addeventlistener) event of WebRTC to end the call, using the [destroy](../webrtc/metodos.md#destroy) method. Otherwise, the call will remain active.
{% endhint %}

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('join', event => {
    const { accessToken } = event.detail;
    const webrtc = new WebRTC();
    await webrtc.create(accessToken);
});
[REPLACE_CODE_FORMAT]

{% content-ref url="../webrtc/" %}
[webrtc](../webrtc/)
{% endcontent-ref %}

## `modify`

This event is triggered when the `modify` method has been called. The event contains the `action` to be taken and the `accessToken`.

{% hint style="warning" %}
It is important to always have `v-schedule-action` and `v-schedule-auth` available in the URL, or the same keys in `localStorage`. Otherwise, we will not be able to detect and emit this event.
{% endhint %}

[REPLACE_CODE_FORMAT]javascript
calendar.addEventListener('modify', event => {
    const { action, accessToken } = event;
});
[REPLACE_CODE_FORMAT]

Based on the action, you should display the option to cancel or reschedule. The `action` key can be:

* `join`: Indicates the desire to join the meeting
* `modify`: Indicates the desire to modify the appointment

{% hint style="info" %}
Here you should use the `cancel` and `reschedule` methods.
{% endhint %}
