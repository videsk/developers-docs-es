---
description: Store your recordings in your own environment hosted on Amazon AWS S3
---

# AWS S3



{% hint style="warning" %}
Once the credentials are entered, they will not be visible again, so you will only be able to overwrite them.
{% endhint %}

{% hint style="info" %}
To integrate Amazon S3, you will need to create an access point from your bucket settings in the **Access Points** menu.
{% endhint %}

## Configuration Suggestions

You should create an exclusive IAM profile for the connection with which you can perform access traceability and action limitations on your S3 bucket.

* We suggest enabling IAM permissions for S3 with write access in **PutObject**.
* Add an ARN with the bucket name and activate the checkbox for any object name.

{% hint style="danger" %}
Do not create an IAM profile with full access, **protect your assets**.
{% endhint %}

You can copy and paste this policy into the IAM JSON editor, **remember to replace your bucket name**.

[REPLACE_CODE_FORMAT]json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "16933222-fba4-4de3-bf3e-427759b73a9d",
            "Effect": "Allow",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<REPLACE_BUCKET_NAME>/*"
        }
    ]
}
[REPLACE_CODE_FORMAT]

<figure><img src="../../.gitbook/assets/Captura desde 2022-09-24 21-30-32.png" alt=""><figcaption><p>You should see a similar configuration</p></figcaption></figure>

Finally, after creating the policy, you should go to the **Security Credentials** tab and then click on the **Generate Access Keys** button.

## Access key ID

Corresponds to the `accessKeyId` provided by AWS S3 when you create a bucket.

## Secret access key

Corresponds to the secret access key (`secretAccessKey`) provided by AWS S3 for external connection to the bucket.

## Region

This is the name of the region provided by AWS S3 at the time of connection. Example: `us-west-1`

## Bucket name

Corresponds to the name of the created bucket. Example: `videsk-storage-s3`

## Security Suggestions

If you are using a multipurpose bucket, we suggest adding access control policies to your buckets to avoid unwanted access to other files.

In the following example, we use an IAM profile `videsk-connector` to define write rules in the folder (prefixes) [`uploads/`](#user-content-fn-1)[^1] , being `ACCOUNT-ID-WITHOUT-HYPHENS` your account ID.

{% hint style="info" %}
Remember to replace the example values with your settings.
{% endhint %}

[REPLACE_CODE_FORMAT]json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPrefixedWrites",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::ACCOUNT-ID-WITHOUT-HYPHENS:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/uploads/*"
        },
        {
            "Sid": "DenyNonPrefixedWrites",
            "Effect": "Deny",
            "Principal": {
                "AWS": "arn:aws:iam::ACCOUNT-ID-WITHOUT-HYPHENS:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*",
            "Condition": {
                "StringNotLikeIfExists": {
                    "s3:prefix": [
                        "uploads/*"
                    ]
                }
            }
        }
    ]
}
[REPLACE_CODE_FORMAT]

Reference: [https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html)

[^1]: This is the file prefix
