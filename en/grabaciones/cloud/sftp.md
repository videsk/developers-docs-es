---
description: Store your recordings in your own environment hosted on an SFTP server.
---

# SFTP

The necessary FTP credentials are as follows:

{% hint style="warning" %}
For security reasons, once credentials are entered, they cannot be viewed again, so you can only overwrite them.
{% endhint %}

## Host

Refers to the domain (FQDN) or IP address of the target server. Example: `sftp.example.com`

{% hint style="info" %}
Enter the domain or IP address without the port.
{% endhint %}

## Username

Refers to the authorized username to upload the files. Example: `videsk`

{% hint style="warning" %}
We suggest creating this user with write permissions in a specific path.
{% endhint %}

{% hint style="danger" %}
For security reasons, we deny the use of the `root` user. Avoid using a superuser.
{% endhint %}

## Port

Refers to the port of the destination FTP server. Example: `21`

{% hint style="info" %}
By default, the value is port 21.
{% endhint %}

## TLS

Enables or disables the connection using TLS verification.

{% hint style="info" %}
We recommend using connections with TLS enabled, which allows us to ensure an encrypted connection between our servers and the destination.
{% endhint %}
