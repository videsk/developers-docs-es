---
description: >-
  Javascript SDK to render forms and surveys created in your account.
---

# 📄 Forms

{% hint style="warning" %}
Forms SDK documentation and assets are strictly restricted to Videsk's customers. We reserve the right to restrict access and usage if we detect a misuse.
{% endhint %}

## Installation

To use Forms SDK you can install it through our CDN.

{% tabs %}
{% tab title="HTML" %}
```html
<link rel="stylesheet" href="https://cdn.videsk.io/sdk/forms.min.css" />
<script src="https://cdn.videsk.io/sdk/forms.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const link = document.createElement('link');
link.rel = "stylesheet";
link.href = "https://cdn.videsk.io/sdk/forms.min.css";
document.head.appendChild(link);

const script = document.createElement('script');
script.src = 'https://cdn.videsk.io/sdk/forms.min.js';
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You must load both CSS and JS assets, otherwise Forms won't work properly.
{% endhint %}

## Usage

{% code lineNumbers="true" %}
```javascript
const form = new FormSDK({ target: document.querySelector('#form-container') });
```
{% endcode %}

You can simply instantiate Forms, and then you should define event listeners and attach methods to a custom button.

## Properties

### `data`

With this property you can get the form with its fields without calling the `submit` method.

```javascript
form.data
// output
  [{...}]
```

## Methods

Once the SDK is instantiated you can access the following methods:

### `on`

This method aims to define a listener when an event happens. The two arguments it receives are:

* `event`: name of the event
* `callback`: function to be executed when the event occurs

```javascript
form.on('submit', callback);
```

### `render`

With this method you render the form fields. The two arguments it receives are:

* `form`: array of fields obtained through [SDK](phone/#get-a-form) or API
* `readonly`: defines if they are read-only or writable, `false` by default

```javascript
form.render(values);
```

### submit

This method allows to submit the form, triggering fields validation and then the `submit` event.

You can obtain the values of the fields and its validity through an `object` return type containing `data` (array) and `valid` (boolean).

```javascript
const response = form.submit();
const { data, valid } = response;
```

{% hint style="info" %}
We suggest you to work with events, since you will have more control over the `submit` actions of the form. **Avoid using the return values**.
{% endhint %}

### `set/update`

With this method you can update the **value of a specific field** through its properties such as: `name`, `label`, `type`, `value` and `_id`. This method receives four parameters:

* **`name`**: value with which the field is going to be searched
* **`value`**: value to insert into the field
* `property`: property to modify, `value` by default
* `key`: name of the property to search for, `name` by default

{% tabs %}
{% tab title="Set value" %}
```javascript
form.set('customer_email', 'john@example.com');
```
{% endtab %}

{% tab title="Required field" %}
```javascript
form.set('customer_email', true, 'properties.required', 'name');
```
{% endtab %}

{% tab title="Read-only field" %}
```javascript
form.set('email', true, 'properties.readonly', 'type');
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
We have a wrapper method that may make the usage easier.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
// Update by field name
form.update('value', 'john@example.com').of('customer_email');
form.update('value', 'john@example.com').of('customer_email', 'name');
// Update by _id
form.update('properties.required', true).of('60fb2623854bb563f843ba09', '_id');
```
{% endcode %}

### `destroy`

This method completely removes the HTML node where it was rendered.

```javascript
form.destroy();
```

{% hint style="info" %}
We suggest you to use this method as a good practice once you don't need the form, that is, it is successfully submitted.
{% endhint %}

## Events

The available events are `submit`, `ready`, `updated`, `error`.

### `submit`

This event occurs once the `submit()` method is executed. The only callback argument is an `object` composed of:

* `valid`: boolean indicating if all the fields are valid

```javascript
form.on('submit', (event) => {
  const { valid } = event;
});
```

{% hint style="info" %}
You must use [Captcha](captcha.md) with this event **if it's a form**, not a survey.
{% endhint %}

{% hint style="warning" %}
[Captcha](captcha.md) is not optional for forms, except surveys.
{% endhint %}

### `ready`

With this event you can listen when the form has been successfully rendered. It contains no callback argument.

```javascript
form.on('ready', () => {});
```

### `updated`

With this event you can listen to a field's value update. The callback argument is an `object` composed of:

* `_id`: corresponds the updated field's id as `string`.
* `value`: corresponds to the field's value, which can be `string`, `boolean`, `array` or `number`.

```javascript
form.on('updated', event => {
  const { _id, value } = event;
});
```

### `error`

With this event you can listen to errors that could only arise when rendering the form. It contains three arguments composed of:

* `name`: error's name as `string`
* `code`: error's code can be `400` and `403`
* `message`: human-readable message for the error

{% hint style="info" %}
This could only **happen if you insert a form created manually**. We recommend always managing the forms from your [dashboard](https://app.videsk.io/forms).
{% endhint %}

```javascript
form.on('error', (name, code, message) => {
// Catch with ingestor or similar
});
```

## Example

```javascript
const form = new FormSDK({ target: document.querySelector('#form-container') });

// Listen when submit the form
form.on('submit', ({ valid }) => {
  if (valid) doSomething();
});

// Attach submit to custom button
document.querySelector('#myButton').addEventListener('click', () => form.submit());

// Render the form
form.render(arrayWithFormElements);
```