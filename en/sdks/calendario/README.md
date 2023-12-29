---
description: We explain how to use our Calendar SDK.
---

# 📅 Calendar

With this SDK, you can embed and programmatically design calendars for scheduling, without worrying about connections, parameters, exceptions, etc.

In other words, we have created this "plug and play" to easily use with a fast-learning structure, without sacrificing the flexibility and power of our API.

{% hint style="info" %}
This SDK does not provide an interface, meaning there is no HTML code, so you will need to manage your own interface, whether in pure HTML, Javascript, or with frameworks like Vue, React, Angular, Svelte, etc.
{% endhint %}

## Installation

To start, you will need to install our resource on your website or mobile application. You have the following alternatives.

{% tabs %}
{% tab title="HTML" %}
[REPLACE_CODE_FORMAT]html
<script src="https://cdn.videsk.io/sdk/calendar.min.js"></script>
[REPLACE_CODE_FORMAT]
{% endtab %}

{% tab title="Javascript" %}
[REPLACE_CODE_FORMAT]javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/calendar.min.js";
document.body.appendChild('body'); // Or replace with the DOM node you wish
[REPLACE_CODE_FORMAT]
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Do not store the script content on your server, **this infringes our terms of use**.
{% endhint %}

{% hint style="danger" %}
For security and quality of service, we have a limit of requests per second per IP/Token, which consists of 20 requests in 1 second. Avoid exceeding this limit, as our Rest API will block requests from your clients.
{% endhint %}

## Instantiate

The first thing you need to do is instantiate a `Calendar` class. The first argument corresponds to the integration token you get from your account.

[REPLACE_CODE_FORMAT]javascript
const calendar = new Calendar(token);
[REPLACE_CODE_FORMAT]

Then you can access its methods and properties.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Methods</strong></td><td>Learn how to use the Calendar SDK methods.</td><td></td><td><a href="metodos.md">metodos.md</a></td><td></td></tr><tr><td><strong>Properties</strong></td><td>Learn what the properties of the Calendar SDK are.</td><td></td><td><a href="propiedades.md">propiedades.md</a></td><td></td></tr></tbody></table>

## Flows

Below, you can see the two types of existing flows, scheduling and modification. We suggest you read carefully so you will have a global view of each step involved in scheduling.

### Scheduling

This flow corresponds to the initial one, when a client wishes to schedule a meeting for the first time.

{% hint style="warning" %}
The sending of reminders can happen up to 4 times at different periods according to the configuration made, both for the client and the agent.
{% endhint %}

{% hint style="info" %}
Possible errors that may arise include scheduling a few seconds before the selected time, for example: Scheduling for 14:05:00 at 14:04:59.



It is also possible that scheduling is denied if someone else has taken the time at the same time, only if there is 1 agent or time available.
{% endhint %}

{% @figma/embed fileId="I4Pe99i1sfDlqRhyl2sgnh" nodeId="0:1" url="https://www.figma.com/file/I4Pe99i1sfDlqRhyl2sgnh/Calendar-flow?node-id=0:1&t=QQPfsWmKEvrPVXfc-1" %}

### Modification

This flow corresponds to when a client wishes to cancel or reschedule a previously requested appointment.

{% hint style="warning" %}
This flow should always be carried out with the tokens sent by email or other selected means. For security, there are no PINs, keys, or searches by email to make modifications.
{% endhint %}

{% @figma/embed fileId="I4Pe99i1sfDlqRhyl2sgnh" nodeId="9:44" url="https://www.figma.com/file/I4Pe99i1sfDlqRhyl2sgnh/Calendar-flow?node-id=9:44&t=QQPfsWmKEvrPVXfc-1" %}
