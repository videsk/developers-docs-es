---
description: >-
  You’ll learn basic and advanced concepts about our webhook-based technology as an integration.
---

# 👓 Introduction

Webhooks are events on a platform that allow an action to be executed when they happen and send data to third parties. For example, when a new call happens within Videsk, that data can be sent to other platforms to sync it.

In other words, these actions are HTTP requests that will run when certain specific events occur and will be sent to a Rest API of your choosing.

While this allows platforms to be integrated with third parties that have a Rest API, most of them require an intermediate step that usually entails investing time and money. This intermediate step is what we call a `transformer/translator`. Let’s look at an example to understand it better.

## How do platforms work today?

If we want to integrate with the [Airtable](https://airtable.com) platform from our platform SuperCall _(fictitious name)_, we will need to understand what and how the [Airtable](https://airtable.com) Rest API receives data.

[Airtable](https://airtable.com) tells us we must send data to its Rest API under the following structure:

```json
{
  "fields": {
    "Name": "John",
    "Last Name": "Doe",
    "Email": "john.doe@example.com"
  }
}
```

But our platform SuperCall _(fictitious name)_ sends data in this other structure:

```javascript
[
  { name: "Name", value: "John" },
  { name: "Last Name", value: "Doe" },
  { name: "Email", value: "john.doe@example.com" }
]
```

**They are not the same! And that's a problem!** Since SuperCall _(fictitious name)_ gives us the option to send data but in its own structure, not like Airtable has to receive it! In other words, **both platforms speak different languages**.

Here are two possible solutions:

1. SuperCall _(fictitious name)_ integrates natively with Airtable. (But it will depend on the time of the SuperCall team to do this) 🥱😴
2. Create an intermediary server that can transform/translate (ETL) the structure and send it correctly. 💵🥵

In real life, both of these solutions take a lot of time and money and are usually discarded, failing with integrations in the short term. 😫

{% hint style="info" %}
Mostly, webhooks function by sending data to a recipient but **do not guarantee** that the recipient will understand that data and structure.
{% endhint %}

**But this is where Videsk has innovated!** :tada:

## Webhooks + ETL = ZeroETL 😎

While webhooks or event-based data exchange has been around for a while, we’ve focused on the biggest pain point for many businesses. **The interoperability of platforms without much effort.**

In order to do this, **we’ve created a mutator and translator that allows our clients to mutate and translate the data, and send it in the format and structure that the destination platform should receive, or in other words, Zero ETL.**

In this way, Videsk is compatible with almost any platform that has an API Rest, SOAP, GraphQL, or, by default, can receive HTTP requests.

Using the previous Airtable example, this is how it would work:

```handlebars
⏬ Format that Airtable expects to receive
{
    "fields": {
        "Name": "John",
        "Last Name": "Doe",
        "Email": "john.doe@example.com"
    }
}
-----------------------------------------------
⏬ Original Videsk format
[
    { name: "Name", value: "John" },
    { name: "Last Name", value: "Doe" },
    { name: "Email", value: "john.doe@example.com" }
]

⏬ Videsk Webhook format (Here's where the magic happens) <<<<<<
{
"fields": {{#object fields}}name,value{{/object}}
}
------------------------------------------------
⏬ Format sent to Airtable
{
    "fields": {
        "Name": "John",
        "Last Name": "Doe",
        "Email": "john.doe@example.com"
    }
}
```

What you see is that from a completely different structure, using our transformation and translation syntax, you can send data as Airtable or any other platform requires.

That is to say, the body of the request (`body`) with the original Videsk format will be transformed and translated based on the data template that you write.

**And so, in a very simple way, you will know that you will practically be able to integrate Videsk with anything!**