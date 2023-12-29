---
description: >-
  Explaining how our webhooks work from a security perspective.
---

# 🔒 Security

Our webhooks technology enables maximun flexibility and compatibility with any modern or legacy platform. At the same time, this means that security is a fundamental pillar when using this feature.

For this reason, we suggest you read carefully the following recommendations and information on how our technology works.

## Secrets

Secrets allow you to securely store sensitive information such as private keys, tokens, usernames, passwords, etc. That is, any information that should not be visible to anyone, **ever**.

Therefore, you have the option of adding an unlimited amount of secrets, and it is your responsibility to determine when something should be a secret or not.

{% hint style="info" %}
Using secrets does not impact performance when sending event data to a platform.
{% endhint %}

**Once the secrets are created, they cannot be seen by anyone ever again, not even by the user who created them.**

If you need to view the value of a secret, you must try to obtain it from the issuing platform. For security reasons, secrets are encrypted at rest and are only decrypted at runtime when they are sent.

**The encryption keys are stored securely and no Videsk personnel has access to them.**

The encryption used for storing secrets at rest is AES-256-CBC.

{% hint style="info" %}
Secrets have a maximum limit of 2000 characters.



If you need to increase this size, contact us at **support@videsk.io**.
{% endhint %}

## Authentication or authorization

We recommend using platforms that have authentication or authorization mechanisms using tokens or unique keys.

{% hint style="info" %}
Videsk supports basic _username:password_ authorization headers.
{% endhint %}

To do this, visit the developer documentation of the platform you want to integrate and look for the authentication or authorization section. For example, most platforms will provide you with an API key which must be sent in the request header or in some cases as a parameter in the URL.

The most common way is to create a header called `Authorization` which must contain the authorization value.

{% hint style="info" %}
We do not provide IP ranges as they are dynamic and global, which allows us to scale and avoid blocking by our clients' platforms.
{% endhint %}

## Best practices

{% hint style="danger" %}
Using our API in the URL is forbidden, your account will be suspended indefinitely if you try to generate a self-inflicted DoS attack.
{% endhint %}

### Authentication or authorization

Do not use our IPs to authorize or validate data sending, as they are dynamic and could eventually be used by other services outside Videsk.

{% hint style="info" %}
Always prefer to use public/private keys.
{% endhint %}

### Rate limit

Check with the platform you want to integrate what is the limit of requests per unit of time. Videsk cannot control the number of requests per unit of time, since it will largely depend on the activity of calls, rows, etc.

{% hint style="info" %}
We try to send requests from different IPs to avoid massive blocking.
{% endhint %}

### Errors

You can debug the errors that may arise during the sending of webhooks through the error logs that we have incorporated. By default, we try to sanitize the data such as headers, parameters, conditional, body of the request, etc. replacing the values of the secrets with asterisks `******`.

{% hint style="warning" %}
For security reasons, we do not sanitize application responses. So, if it returns sensitive information, you should inform them about it.
{% endhint %}

### Testing

Verify the format generated in our built-in editor before sending it to the original platform, this way you will avoid crashes or eventually marking your account as suspicious.

Additionally, we suggest you use playground platforms like the ones mentioned here to avoid constant requests with errors.

{% content-ref url="integrations/" %}
[Integrations](integrations/)
{% endcontent-ref %}

### SSL

An option available in webhooks is to disable SSL validation. By default, we verify that the SSL of the endpoint is valid as a security measure, this way we can ensure that the data transportation is encrypted between our servers and those of the platform in question.

If you need to, you can disable the verification, but this will cause the data transportation to eventually not be secure if the platform's SSL is not valid.

{% hint style="info" %}
If you have the option to verify SSL enabled and you see certificate errors, you should contact the platform to verify that its certificate is valid.
{% endhint %}

{% hint style="success" %}
We recommend that you always verify that the communication protocol in the URL begins with `https://`, otherwise the communication will not be encrypted.
{% endhint %}

## Infrastructure

Our webhooks infrastructure was designed with security as the number one pillar. We use serverless technology which allows us to scale to millions of requests per second and generating an isolation of all the requests that are made in our platform.

This design was thought of in the face of possible attacks from our platform towards third parties or even remote code execution.

Our serverless instances only run for a maximum of 60 seconds, destroying all information at runtime, with no memory relation between requests. If a request takes more than 30 seconds to respond, it will be canceled and an error will be returned that you can view in the logs.

Everything runs within our VPC network and exits once the request is completely ready.

{% hint style="info" %}
The average transfer speed between commercial platforms does not exceed 250 milliseconds.
{% endhint %}