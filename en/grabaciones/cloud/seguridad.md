---
description: >-
  Below we explain the security applied to the recording function.
---

# Security

We explain how we operate at the security level with the recordings both in runtime and in storage (at rest).

{% hint style="info" %}
We are writing the documentation on our procedures and designs of this function in terms of security.
{% endhint %}

## Credentials

All credentials are securely stored as private keys, tokens, usernames, connection URLs, etc. That is, all information that should not be visible to anyone, **ever**.

{% hint style="info" %}
We access the credentials only at runtime in an isolated manner, allowing all traces from memory to be purged after the recordings are uploaded. **No Videsk staff has access to them.**
{% endhint %}

The encryption and decryption used for the storage of credentials at rest is AES-256-CBC.

In the following scheme, we explain how the process of storing and transacting the credentials is carried out.

{% @figma/embed fileId="0vs8s1P47jsMfMMA2Ktpgt" nodeId="101:2" url="https://www.figma.com/file/0vs8s1P47jsMfMMA2Ktpgt/Recordings?node-id=101%3A2" %}

{% hint style="info" %}
The credentials have a maximum limit of 5000 characters.

If you have an x509 certificate or similar of greater length, you can increase this size by contacting us at **support@videsk.io**.
{% endhint %}

## Infrastructure

The recording infrastructure was designed with security as the number one pillar. We use `realtime` technology to record video calls and each video/audio of each participant, which allows us to scale to millions of recordings in parallel and create isolation of all recordings made on our platform.

Temporary or persistent storage is done on our private infrastructure, where only certain Videsk employees have access depending on their roles such as DevOps or cybersecurity. Being only permissions for changing bucket configurations and data replication without being able to view or modify them.

## Redundancy

All recordings are backed up in our infrastructure temporarily or persistently.

Only if you configure backup in third-party clouds, after confirming the successful upload, we delete the backup entirely, otherwise, we maintain a backup accessible from your dashboard so that you can later request manual sending.

This configuration allows us to provide redundancy over the recordings to avoid unwanted losses, should your storage provider fail.

{% hint style="info" %}
We perform a minimum billing of 100GB to ensure redundancy availability for your account.
{% endhint %}

## Integrity

We verify the integrity of the recordings and files using cryptography by generating and verifying SHA-256, and for integrity verification in transit, we use cyclic redundancy check or CRC-32.

This allows us to ensure the integrity of the recordings at rest and in transport, thus mitigating attacks such as Man-in-the-middle, mutations, or similar.

{% hint style="info" %}
You can verify the hash of each file after downloading.
{% endhint %}
