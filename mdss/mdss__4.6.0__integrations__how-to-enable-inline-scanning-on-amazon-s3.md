<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-enable-inline-scanning-on-amazon-s3 -->

# How to Enable Inline Scanning?

In order to prevent access to files on AWS S3 that have not been scanned yet, a bucket policy can be used in combination with the [file tagging](https://www.opswat.com/docs/mdss/configuration/file-tagging) feature in MDSS to only allow get requests on files with the "No Threat Detected" tag.

For example, a bucket policy allowing full access just to scanned files would look like this:

```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": [
    "s3:*"
  ],
  "Resource": [
    "arn:aws:s3:::<BUCKET_NAME>/*",
    "arn:aws:s3:::<BUCKET_NAME>"
  ],
  "Condition": {
    "StringEquals": {
      "s3:ExistingObjectTag/MetaDefenderResult": "No Threat Detected"
    }
  }
}
```

In the above example `<BUCKET_NAME>`  should be replaced with the S3 bucket name configured in MDSS or with the corresponding folder path that is subject to scanning.

The "Action" list from the example above can also be customized to only allow specific actions on the objects in question. To allow just get operations on scanned objects the `s3:GetObject` action can be used instead of `s3:*` .

This approach is particularly useful when using [event-based real time scanning](https://www.opswat.com/docs/mdss/configuration/event-based-handling) as it prevents any uploaded file from being accessed while it's still processing in MDSS.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
