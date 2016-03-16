---
layout: post
title: Copy S3 bucket to another AWS account
---

I recently had to copy an S3 bucket from one account to another. Here"s
the steps required.








In the AWS account you want to **copy from**, allow the account you want
to copy to access.










    {
        "Version": "2008-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Sid": "AccountBAccess1",
                "Principal": {
                    "AWS": "XXXXXXXX"
                },
                "Action": "s3:*",
                "Resource": "arn:aws:s3:::BUCKET_NAME/*"
            }
        ]
    }

Next configure the aws-cli (brew install awscli) to use the new AWS
account credentials (you"ll need to create a user and give them full S3
access).

Now you can use s3
[sync](http://docs.aws.amazon.com/cli/latest/reference/s3/sync.html) to
sync across aws accounts.

    aws s3 sync s3://oldbucket s3://new-bucket



 









