---
description: >-
  You will find below some information on how to debug errors in webhooks.
---

# 🐞 Errors

In the functions you will find in webhooks, error logs are those that can provide you with information related to requests that have been sent and may have failed, either in the process of mutation, on the network (sending), or if the platform has responded with an error.

This way you can easily identify what is not working correctly in integrations.

This feature is enabled by default and cannot be disabled.

{% hint style="info" %}
The logs last for 30 days from the moment they are created, after which they are automatically deleted.

If you need to keep the logs longer, send us an email at support@videsk.io.
{% endhint %}

{% hint style="warning" %}
**We only detect errors with status codes 4XX or higher.** If the platform to be integrated responds with errors with status codes 2XX, they will not be considered errors.

In the case of format errors in the webhook, we will automatically capture the error.
{% endhint %}

## Structure

The errors captured during the sending process contain a structure that can be easily visualized.

![Error structure](<../.gitbook/assets/image (56).png>)

By default you will be able to see the following data, which we will describe below.

### Context

This information is about the event as a trace ID `traceId` and the date it was generated `createdAt`.

### Request

This information contains request data such as:

#### URL

This value corresponds to the URL you have entered in the webhook configuration.

#### Method

This is the method with which the request was sent which can be `POST`, `GET`, `PATCH`, `PUT`, `HEAD`, `OPTIONS` or `DELETE`.

#### Source

This value corresponds to the source of the error, which can be `parsing`, which corresponds to the syntax `{{mustache}}` or `third-party` which would be errors caused in responses from the external platform such as `4XX` or `5XX`.

{% hint style="warning" %}
Remember, we only detect errors with status codes 4XX or higher.
{% endhint %}

#### SSL

Boolean value if SSL certificate was verified or not.

### Headers

These values are dynamic, since they correspond to the headers you have configured in the webhook. By default, `Content-Type` is mandatory.

### Parameters

These are dynamic values, since they correspond to the parameters for the url that you have configured in the webhook.

### Response

In case of a `third-party` source error, there will be data such as:

#### Status code

This is the HTTP status code that the platform has responded to, such as `4XX` or `5XX`.

#### Status name

This is the name of the HTTP status code, such as `BadRequest`, `NotAuthenticated`, `ServerError`, etc.

### Error

This value is of greater relevance as it will indicate the error that has occurred, both if it is a syntax error and if it is an error that the platform to be integrated has responded to.

It is possible that a platform does not always respond with content, therefore this value could be empty.

{% hint style="info" %}
Remember to compare this value by comparing the `source` parameter to identify the cause of the error.
{% endhint %}

###

### Payload

This is the unmutated value, that is, with the pure syntax.

{% hint style="info" %}
We store this value to maintain its atomicity and avoid confusion if you edit the webhook.
{% endhint %}