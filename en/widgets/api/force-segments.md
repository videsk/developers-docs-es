# Force segments

With this function you can force the enumeration of segments in your widget in a very simple way. That is, it will overwrite the list of public segments that appear in the widget with the ones you define using this method.

## How to use

The first thing you must do is look for the ID of the segment or segments in your dashboard account. Then you must generate a list (`Array`) with them:

```javascript
[
  { name: "Segment Name", id: "635c836300f9e8246a0f95f2" },
  { name: "Segment Name 2", id: "635c837e2f38b41ad2143b71" },
]
```

{% hint style="info" %}
You must replace the name in `name` and paste the ID of the segment in `id`.
{% endhint %}

Finally, you need to save the generated list to the local storage `localStorage`.

```javascript
const segments = [...];
window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
```

## Example

This example is functional, so you should only change the name of the segment and paste the corresponding ID.

{% hint style="info" %}
Remember that you can use one or more segments.
{% endhint %}

{% tabs %}
{% tab title="Javascript" %}
{% code title="Pure javascript" lineNumbers="true" %}
```javascript
const segments = [
  { name: "My segment", id: "635c843f35f1254a417612d9" }
];
window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
```html
<script>
    const segments = [
        { name: "My segment", id: "635c843f35f1254a417612d9" }
    ];
    window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
</script>
```
{% endtab %}
{% endtabs %}