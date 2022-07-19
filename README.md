## next-sync-s3

### Github Actions secrets

- AWS_ACCESS_KEY_ID
- AWS_CLOUD_FRONT_DISTRIBUTION
- AWS_REGION
- AWS_S3_BUCKET
- AWS_SECRET_ACCESS_KEY

### IAM ROLE POLICY

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:ListBucket",
        "s3:DeleteObject",
        "cloudfront:CreateInvalidation",
        "s3:PutObjectAcl"
      ],
      "Resource": [
        "arn:aws:cloudfront::{YOUR_AWS_ACCOUNT_ID}:distribution/{YOUR_AWS_CLOUD_FRONT_DISTRIBUTION}",
        "arn:aws:s3:::{YOUR_AWS_S3_BUCKET}/*",
        "arn:aws:s3:::{YOUR_AWS_S3_BUCKET}"
      ]
    }
  ]
}
```

### S3

#### access control list (ACL)

- Bucket owner (your AWS account)
  - Objects
    - List
    - Write
  - Bucket ACL
    - Read
    - Write
- Everyone (public access)
  - Read

#### Bucket policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity {YOUR_OAI}"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::{YOUR_AWS_S3_BUCKET}/*"
    }
  ]
}
```

### CloudFront Distributions

#### General Settings

Default root object: `index.html`

#### Origins

- S3 bucket access: Yes use OAI
- Bucket policy: No, I will update the bucket policy
