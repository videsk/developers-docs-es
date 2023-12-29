---
description: >-
  Learn how to sync recordings with local download to an AWS S3 bucket
---

# AWS S3

{% hint style="warning" %}
Remember that it is your responsibility to restrict access to the recordings in an AWS S3 bucket.
{% endhint %}

{% hint style="danger" %}
We strongly recommend managing credentials correctly by restricting access to write-only, without reading or modifying existing files, along with policies for `.mp4` and `.webm` extensions.
{% endhint %}

Before configuring the folder to sync, we recommend setting up the download location for the agent's browser recordings.

{% content-ref url="ubicacion-de-descargas.md" %}
[ubicacion-de-descargas.md](ubicacion-de-descargas.md)
{% endcontent-ref %}

## S3 Browser

This free S3 manager with an interface allows you to manage a bucket, define permissions, and create a synchronization of local files to S3.

{% hint style="info" %}
Only available for Windows.
{% endhint %}

For this, we suggest going to the [download page](https://s3browser.com/download.aspx) and then read the documentation on [how to sync a local folder to S3](https://s3browser.com/amazon-s3-folder-sync.aspx) securely.

{% hint style="danger" %}
We suggest restricting permissions to write-only and, if possible, to `.webm` and `.mp4` extensions.
{% endhint %}

## AWS CLI

AWS CLI is an official AWS tool that allows managing S3 buckets through command line.

For this, go to the [AWS CLI page](https://aws.amazon.com/es/cli/) and install the tool on the computers.

We suggest watching the following video from teckno.net where he explains how to set up `AWS CLI` for syncing local files to an S3 bucket.

Or you can directly access their post: [https://www.tekco.net/?p=1590](https://www.tekco.net/?p=1590)

{% embed url="https://www.youtube.com/watch?v=3vpcsvNZQsY" %}

{% hint style="warning" %}
Remember to securely store S3 credentials through encryption.
{% endhint %}

{% hint style="info" %}
If you have any questions, you can contact us at [support@videsk.io](mailto:support@videsk.io).
{% endhint %}
