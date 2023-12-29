# 🔇 Noise Cancellation

{% hint style="danger" %}
The source code is property of Videsk. Usage is restricted to active Videsk clients, and copying, modifying, or using without authorization is legally punishable.
{% endhint %}

{% hint style="info" %}
If you wish to use this SDK, please contact us at [support@videsk.io](mailto:support@videsk.io) or your account executive to authorize access.
{% endhint %}

With this SDK, you can cancel ambient noise, amplifying the voice coming from the device's microphone.

## Considerations

{% hint style="info" %}
This SDK operates through deep learning and recurrent neural networks, which consume more CPU/GPU. You should consider the device's performance before using this feature.
{% endhint %}

This SDK is designed for use only in controlled ambient noise contexts, not for construction sites, concerts, or factories. Although it will apply noise cancellation, you will not get the best result.

{% hint style="info" %}
The ideal ambient noise should be less than or equal to 90 db (decibels).
{% endhint %}

As a reference, you can use this table:

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Source: <a href="https://es.wikipedia.org/wiki/Decibelio">https://es.wikipedia.org/wiki/Decibelio</a></p></figcaption></figure>

## Usage

According to the private instructions we have given you, you should use the SDK as follows:

[REPLACE_CODE_FORMAT]javascript
const suppression = new NoiseSuppression();
[REPLACE_CODE_FORMAT]

Then, you should use the available methods and properties.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Methods</strong></td><td>Learn how to use the methods of <code>NoiseSuppression</code>.</td><td></td><td><a href="metodos.md">metodos.md</a></td></tr><tr><td><strong>Properties</strong></td><td>Find out what the properties of <code>NoiseSuppression</code> are.</td><td></td><td><a href="propiedades.md">propiedades.md</a></td></tr></tbody></table>
