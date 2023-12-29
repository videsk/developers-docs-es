---
description: Learn to use variables to integrate Videsk with third parties.
---

# 🦱 Variables

Variables, as you may know, allow you to store data and reuse it in different parts of the code.

In the case of our Webhooks, they allow you to inject variables that will depend on conditions, states, etc.

For example, this sentence that indicates an order has two variables:

```handlebars
Computer executes {{action}} within {{period}} days.
```

Depending on the value of `action` and `period`, the sentence could have different results, but you will always get a sentence with action and period.

## Variables by event

In the case of webhooks, each event has its own variables, something similar to a dictionary of variables by event.

You can find these events directly in edit mode when you create a new webhook. They are located on the side panel, next to the documentation tab.

![Dictionary example](<../.gitbook/assets/image (52).png>)

Because each event has its own variables, you can get information about each one, such as its type, description, and name.

* `type` corresponds to the data type: `array`, `string`, `boolean`, or `object`.
* `description` corresponds to the context of the variable.
* `name` corresponds to the name of the variable.

{% hint style="warning" %}
In the case of `array` variables, you can only access them using `#array` helpers or by specifying the index you want to get in Handlebars syntax.
{% endhint %}