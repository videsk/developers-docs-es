---
description: Store your recordings in your own environment hosted on Azure Blob
---

# Azure

{% hint style="warning" %}
Once credentials are entered, they cannot be viewed again, so you can only overwrite them.
{% endhint %}

The credentials needed to connect the recordings with your Azure environment are:

## Option 1

### Connection String

Azure gives you the possibility to provide a unique connection URL that includes all the necessary credentials for connecting to the storage bucket. This URL contains:

* `AccountName`
* `AccountKey`
* `Protocol`
* `BlobEndpoint`

#### Example:

[REPLACE_CODE_FORMAT]
DefaultEndpointsProtocol=<protocol>;AccountName=<name>;AccountKey=<key>;BlobEndpoint=<endpoint>
[REPLACE_CODE_FORMAT]

### Container Name

This refers to the specific container name in which the uploaded files will be stored.

## Option 2

### Account Name

This refers to the name of the Azure account where the container is located.

### Account Key

This refers to the secret key that grants write permission to the account for the specific container.

### Protocol

This refers to the connection protocol to be used with Azure Blob storage, by default set as `http`, but with the possibility of using `https`.

{% hint style="info" %}
We suggest using a connection via `TLS`, i.e., through an encrypted connection.
{% endhint %}

### Blob Endpoint

This refers to the endpoint provided by Azure where the files will be stored.

### Container Name

This refers to the specific container name in which the uploaded files will be stored.
