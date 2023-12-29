# Methods

## Segments 🚦

With this method you can get the segments of your account to show them to your customers.

{% tabs %}
{% tab title="Request" %}
```javascript
const response = await phone.getSegments();
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
"total": 2,
"limit": 10,
"skip": 0,
"data": [
{
"name": "Segment 1",
"id": "5f7f67333baba9c4818d3a08"
},
{
"name": "Segment 2",
"id": "203e4ffec73a69409edc14ea"
}
],
"cached": true
}
```
{% endtab %}
{% endtabs %}

## Available agents 📞

With this method you can get the total number of available or online agents. It is important that you use this method to notify your customers when there are no available agents.

{% hint style="info" %}
Two arguments are accepted, the first one is the segment ID and the second one is the status that must be checked. This last argument receives the status like **`online`** or **`available`** .

The **`online`** status will deliver the number of connected agents in that segment.

While **`available`** will deliver the number of agents that are ready to receive a call, that is, that are not in a call and connected.
{% endhint %}

{% tabs %}
{% tab title="Request" %}
```javascript
await phone.getAgents(segmentId); // By default = online
await phone.getAgents(segmentId, 'available'); // Will look for the number of agents that are ready to receive a call.
```
{% endtab %}

{% tab title="Response" %}
```javascript
1 // Integer
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The API response will return the total as a number, `integer`. That is, you can store the total directly in a variable. **It's not an object**.
{% endhint %}

{% hint style="warning" %}
By default, if you make a call, the SDK will check that there are agents in online status, otherwise the `no-agents` event will be triggered.
{% endhint %}

## Call ☎

With this method, you can call, indicating the segment from which the call will be made.

```javascript
await phone.call('5f7f67333baba9c4818d3a08');
await phone.connect('5f7f67333baba9c4818d3a08');
// Both methods are equivalent
```

## Abandon&#x20;

With this method you can allow your customers to leave the waiting queue.

{% hint style="warning" %}
You should only use this method when you are in the waiting queue, not before or after.
{% endhint %}

```javascript
phone.leave();
```

{% hint style="info" %}
It is also possible to leave the queue indicating the motive or reason, only if you have configured abandon reasons. To get the abandon reasons [go here](methods.md#get-abandon-reasons).
{% endhint %}

```javascript
const [{ id }] = await phone.getAbandonReasons();
phone.setAbandonReason({ id });
```

{% hint style="danger" %}
You should use the `leave` or `setAbandonReason` method, not both.
{% endhint %}

## Hang up

With this method you can manually hang up the call.

```javascript
phone.hangup();
```

{% hint style="warning" %}
You should use this method in conjunction with the [WebRTC SDK](../webrtc/), listening to the hang up event.
{% endhint %}

```javascript
const events = {
hangup: () => phone.hangup(),
};
const options = { el: '#webrtc' };
let webrtc = new VideskWebRTCSDK(idCall, events, options);
```

## Listen

{% hint style="warning" %}
You can use this method to listen to events or as indicated below.
{% endhint %}

With this method you can assign a callback function to a particular event in the following way:

{% code lineNumbers="true" %}
```javascript
phone.listen(eventName, callback);
// Example
phone.listen('queued', () => console.log('The client has been added to the queue'));
```
{% endcode %}

{% hint style="info" %}
For the following methods you should use our two SDKs [Forms](../forms.md) and [Captcha](../captcha.md), **only if you want to use them**.
{% endhint %}

***

## Get form

With this method you can get the form of a segment. It receives three arguments:

1. Segment ID
2. Version of the form `base` or `contact`, by default `base`
3. Dispatch event `true` or `false` `(optional)`

```javascript
phone.getForm(segmentId, version);
```

{% hint style="info" %}
The output value may be null, meaning there are no associated forms and you can proceed with the call.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
const response = await phone.getForm(segmentId, 'base');
if (!response) return continueWithCall();
// Load Forms SDK
const { form } = response;
```
{% endcode %}

{% code lineNumbers="true" %}
```javascript
const response = await phone.getForm(segmentId, 'contact');
// Load Forms SDK
const { form } = response;
```
{% endcode %}

Example:

{% code lineNumbers="true" %}
```javascript
const totalAgents = await phone.getAgents(segmentId);

if (totalAgents < 1) return showContactFormNotAvailable(segmentId);

const response = await phone.getForm(segmentId, 'base');

if (response) return showBaseFormPreviousCall(response.form);
else continueWithCallWithoutForm();
```
{% endcode %}

{% hint style="danger" %}
If you activate a base form in a segment **you will not be able to continue to the call without a previously submitted form**.
{% endhint %}

## Send form

{% hint style="warning" %}
You should use our [forms](../forms.md) and [captcha](../captcha.md) SDK.
{% endhint %}

With this method you can send a form. Receives one argument as `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong> values,
type,
segment,
token,
}
</code></pre>

* `values` is an array obtained by using the [Form SDK](../forms.md).
* `type` is the type of form that can be `pre-call` or `contact`.
* `segment` is the segment ID to call.
* `token` is a string obtained by using the [Captcha SDK](../captcha.md).

```javascript
const response = await phone.sendForm(data);
const formId = response.submission; // Form id
```

{% hint style="info" %}
The output value may be null, meaning that some of the form fields are invalid or the captcha token has expired.
{% endhint %}

## Get survey

With this method you can get a survey of a segment. It receives a single argument the segment ID:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const response = await phone.getSurvey(segmentId);
</strong><strong>const { form } = response;
</strong></code></pre>

## Send survey

{% hint style="warning" %}
You should use our [forms](../forms.md) SDK.
{% endhint %}

With this method you can send a survey. Receives one argument as `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong> values,
call,
segment,
}
</code></pre>

* `values` is an array obtained by using the [Form SDK](../forms.md).
* `call` is the call ID.

```javascript
await phone.sendSurvey(data);
```

{% hint style="info" %}
The output value may be null, meaning that some of the survey fields are invalid.
{% endhint %}

## Get abandon reasons

With this method you can obtain the abandonment reasons configured in your account.

{% tabs %}
{% tab title="Get" %}
```javascript
const abandonReasons = await phone.getAbandonReasons();
```
{% endtab %}

{% tab title="Response" %}
```javascript
[
{
"label": "Waiting time",
"name": "too-much-wait",
"id": "62ed6b537fb69f6ce50c8539"
},
{
"label": "I resolved my doubts",
"name": "resolve-my-doubts",
"id": "6306422767b540c40429973d"
}
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You must verify that there are abandonment reasons configured in your account, otherwise you will get an error 404.
{% endhint %}