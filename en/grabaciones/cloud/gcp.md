---
description: Store your recordings in your own environment hosted on GCP Storage
---

# GCP

{% hint style="warning" %}
Once credentials are entered, they cannot be viewed again, so you can only overwrite them.
{% endhint %}

## Configuration Suggestions

### 1. Create Role/Function

You should create a new role. To do this, go to IAM, then click on **Create Role**, and fill in the required fields. We suggest entering the role or function name as "Videsk Connector", so you can find it more easily.

In the permissions section, you should click on the **Add Permissions** button, where you will search for **Storage Object Creator**, and finally select the permissions:

* `storage.multipartUploads.create`
* `storage.multipartUploads.abort`
* `storage.objects.create`

Click on **Create**.

{% hint style="info" %}
If your interface is in English, a role corresponds to **Roles** in the IAM menu.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You should use this role to create the credentials in the next step. This ensures that we only have permissions to create files, not read or modify.
{% endhint %}

### 2. Create Credentials

Go to **APIs & Services**, then at the top click on **Create Credentials**, and then on **Service Account**. Enter the required fields, where Service Account Name can be "_Videsk Connector_" and Service Account ID "_videsk-connector-1234_" (_this is optional, you can choose any name_). Click on **Create and Continue**.

Then in the role to select, search for "videsk", and select the role created earlier.

Additionally, you can add an IAM condition, where you limit access to the storage.googleapis.com Service and the bucket name.

If you wish (optional), you can create these conditions by copying and pasting the following snippet into the **Condition Editor**.

[REPLACE_CODE_FORMAT]
resource.service == "storage.googleapis.com" &&
resource.name == "my-bucket-name"
[REPLACE_CODE_FORMAT]

Click on **Continue** and then on the **Done** button.

{% hint style="info" %}
It is not required to grant user access to the service account.
{% endhint %}

Then you should search for the service account by clicking on its name. Subsequently, in the top menu click on keys, **Add Key** > **Create New Key**.

Finally, click on the **JSON** key type.

<figure><img src="../../.gitbook/assets/image (8) (2).png" alt=""><figcaption><p>Generate private key</p></figcaption></figure>

As a last step, you should paste the content of the JSON file into our configuration interface and Test the credentials.

{% hint style="info" %}
You can only test the credentials the first time you create them, then you will not be able to use the function.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

## Option 1

### Bucket Name

Refers to the specific `bucket` name where the files will be stored.

### Key File Credentials

A `JSON` credentials file auto-generated by Google Cloud associated with a service account that has write permissions.

{% hint style="info" %}
This file provides a faster and more secure setup, although it serves the same purpose as separate credentials.
{% endhint %}

#### Example:

[REPLACE_CODE_FORMAT]
{
  "type": "service_account",
  "project_id": "PROJECT_ID",
  "private_key_id": "KEY_ID",
  "private_key": "-----BEGIN PRIVATE KEY-----\nPRIVATE_KEY\n-----END PRIVATE KEY-----\n",
  "client_email": "SERVICE_ACCOUNT_EMAIL",
  "client_id": "CLIENT_ID",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/SERVICE_ACCOUNT_EMAIL"
}
[REPLACE_CODE_FORMAT]

## Option 2

### Project ID

Refers to the ID of the project where the storage `bucket` for the files is located.

### Bucket Name

Refers to the specific `bucket` name where the files will be stored.

### Private Key

A private key granted to the service account with write permission to create files.

### Client Email

The email address of the associated service account that has write permissions.

{% content-ref url="metadata.md" %}
[metadata.md](metadata.md)
{% endcontent-ref %}