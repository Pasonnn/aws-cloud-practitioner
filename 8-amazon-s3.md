# Section 8: Amazon S3

## 72. S3 Overview

### Section Introduction
- Amazon S3 is one of the main building blocks of AWS
- It's advertised as "infinitely scaling" storage
- Many website use Amazon S3 as a backbone
- Many AWS services use Amazon S3 as an integration as well
- We-ll have a step-by-step approach to S3

### Amazon S3 Use cases
- Backup and storage
- Disaster Recovery
- Archive
- Hybrid Cloud storage
- Application hosting
- Media hosting
- Data lakes & big data analytics
- Software delivery
- Static website

### Amazon S3 - Buckets
- Amazon S3 allows people to store objects (files) in "buckets" (directories)
- Buckets must have a globally unique name (across all regions all accounts)
- Buckets are defined at the region level
- S3 looks like a global service but buckets are created in a region
- Naming convention
    - No uppercase, No underscore
    - 3-63 characters long
    - Not an IP
    - Must start with lowercase letter or number
    - Must NOT start with the prefix xn--
    - Must NOT end with the suffix -s3alias

### Amazon S3 - Objects
- Objects (files) have a Key
- The key is the FULL path:
    - s3://my-bucket/my_file.txt
    - s3://my-bucket/my_folder|/another_folder/my_file.txt
- The key is composed of prefix + object name
    - s3://my-bucket/my_folder|/another_folder/my_file.txt
- There's no concept of "directories" within buckets (although the UI will trick you to think otherwise)
- Just keys with very long names that contain slashes ("/")
- Object values are the content of the body:
    - Max. Object Size is 5TB (5000GB)
    - If uploading more than 5GB, must use "multi-part upload"
- Metadata (list of text key/value pairs - system or user metadata)
- Tags (Unicode key / value pair - up to 10) - useful for security / lifecycle
- Version ID (if versioning is enabled)

## 73. S3 Hands On
***This is a lab tutorial lesson***

## 74. S3 Security: Bucket Policy

### Amazon S3 - Security
- User-Based
    - IAM Policies - which API calls should be allowed for a specific user from IAM
- Resource-Based
    - Bucket Policies - bucket wide rules from the S3 console - allows cross account
    - Object Access Control List (ACL) - finer grain (can be disabled)
    - Bucket Access COntrol List (ACL) - less common (can be disabled)
- Note: an IAM principal can access an S3 object if
    - The user IAM permissions ALLOW it OR the resource policy ALLOWS it
    - AND there's no explicit DENY
- Encryption: encrypt objects in Amazon S3 using encryption keys

### S3 Bucket Policies
- JSON based policies
    - Resources: buckets and objects
    - Effect: Allow / Deny
    - Actions: Set of API to Allow or Deny
    - Principal: The account or user to apply the policy to
- Use S3 bucket for policy to
    - Grant public access to the bucket
    - Force objects to be encrypted at upload
    - Grant access to another account (Cross Account)

![S3 Bucket Policies](assets/74-s3-bucket-policies.png)

### Example: Public Access - Use Bucket Policy

![Example of Public Access - Use Bucket Policy](assets/74-example-public-access.png)

### Example: User Access to S3 - IAM permissions

![Example of User Access to S3 - IAM permissions](assets/74-example-user-access-to-s3.png)

### Example: EC2 instance access - Use IAM Roles

![Example of EC2 instance access - Use IAM Roles](assets/74-example-ec2-instance-access.png)

### Advanced: Cross-Account Access - Use Bucket Policy

![Advaned of Cross-Account Access - Use Bucket Policy](assets/74-advanced-cross-account-access.png)

### Bucket settings for Block Public Access

![Bucket settings for Block Public Access](assets/74-bucket-settings-for-block-public-access.png)

- These settings were created to prevent company data leaks
- If you know your bucket should never be public, leave these on
- Can be set at the account level

## 75. S3 Security: Bucket Policy Hands On
***This is a lab tutorial lesson***

## 76. S3 Website Overview

### Amazon S3 - Static Website Hosting
- S3 can host static websites and have them accessible on the Internet
- The website URL will be (depending on the region)
    - http://**bucket-name**.s3-website-**aws-region**.amazonaws.com
    - OR http://**bucket-name**.s3-website.**aws-region**.amazonaws.com
- If you get a **403 Forbidden** error, make sure the bucket policy allows public reads!

![Static Website Hosting](assets/76-static-website-hosting.png)

## 77. S3 Website Hands On
***This is a lab tutorial lesson***

## 78. S3 Versioning Overview

### Amazon S3 - Versioning
- You can version your files in Amazon S3
- It is enabled at the bucket level
- Same key overwrite will change the "version": 1,2,3...
- It is best practice to version your buckets
    - Protect against unintended deletes (ability to restore a version)
    - Easy roll back to previous version
- Notes:
    - Any file that is not versioned prior to enabling versioning will have version "null"
    - Suspending versioning does not delete the previous versions

![Amazon S3 Versioning](assets/78-amazon-s3-versioning.png)

## 79. S3 Versioning Hands On
***This is a lab tutorial lesson***

## 80. S3 Replication Overview

### Amazon S3 - Replication (CRR & SRR)
- Must enable Versioning in source and destination buckets
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3
- Use cases:
    - CRR - compliance, lower latency access, replication across accounts
    - SRR - log aggregation, live replication between production and test accounts

![Amazon S3 - Replication](assets/80-s3-replication.png)

## 81. S3 Replication Hands On
***This is a lab tutorial lesson***

## 82. S3 Storage Classes Overview

### S3 Storage Classes
- Amazon S3 Standard - General Purpose
- Amazon S3 Standard - Infrequent Access (IA)
- Amazon S3 One Zone - Infrequent Access
- Amazon S3 Glacier Instant Retrieval
- Amazon S3 Glacier Flexible Retrieval
- Amazon S3 Glacier Deep Archive
- Amazon S3 Intelligent Tiering

- Can move between classes manually or using S3 Lifecycle configurations

### S3 Durability and Availability
- Durability
    - High durability (99.99%) of objects across multiple AZ
    - If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
    - Same for all storage classes
- Availability:
    - Measures how readily available a service is
    - Varies depending on storage class
    - Example: S3 standard has 99.99% availability = not available 53 minutes a year

### S3 Standard - General Purpose
- 99.99% Availability
- Used for frequently accessed data
- Low latency and high throughput
- Sustain 2 concurrent facility failures
- Use Cases: Big Data analytics, mobile & gaming applications, content distribution...

### S3 Storage Classes - Infrequent Access
- For data that is less frequently accessed, but required rapid access when needed
- Lower cost than S3 Standard
- Amazon S3 Standard-Infrequent Access (S3 Standard-IA)
    - 99.9% Availability
    - Use cases: Disaster Recovery, backups
- Amazon S3 One Zone - Infrequent Access (S3 One Zone-IA)
    - High durability (99.99%) in a single AZ; data lost when AZ is destroyed
    - 99.5% Availability
    - Use Cases: Storing secondary backup copies of on-premise data, or data you can recreate

### Amazon S3 Glacier Storage Classes
- Low-cost object storage meant for archiving/backup
- Pricing: price for storage + object retrieval cost
- Amazon S3 Glacier Instant Retrieval
    - Millisecond retrieval, great for data accessed once a quarter]
    - Minimum storage duration of 90 days
- Amazon S3 Glacier Flexible Retrieval (formerly Amazon S3 Glacier)
    - Expedited (1 to 5 minutes), Standard (3 to 5 hours), Bulk (5 to 12 hours) - free
    - Minimum storage duration of 90 days
- Amazon S3 Glacier Deep Archive - for long term storage:
    - Standard (12 hours), Bult (48 hours)
    - Minimum storage duration of 180 days

### S3 Intelligent-Tiering
- Small monthly monitoring and auto-tiering fee
- Moves objects automatically between Access Tiers based on usage
- There are no retrieval charges in S3 Intelligent-Tiering
- Frequent Access tier (automatic): default tier
- Infrequent Access tier (automatic): objects not accessed for 30 days
- Archive Instant Access tier (automatic): objects not accessed for 90 days
- Archive Access tier (optional): configurable from 90 days to 700+ days
- Deep Archive Access tier (optional): config. from 180 days to 700+ days

### S3 Storage Classes Comparison

![S3 Storage Classes Comparison](assets/82-s3-storage-classes-comparison.png)

### S3 Storage Classes - Price Comparison
**Example: us-east-1**

![us-east-1 S3 Storage Classes Price Comparison](assets/82-s3-storage-classes-example.png)

## 83. S3 Storage Classes Hands On


## 84. S3 Express One Zone


## 85. S3 Encryption


## 86. IAM Access Analyzer for S3


## 87. Shared Responsibility Model for S3


## 88. AWS Snow Family Overview


## 89. AWS Snow Family Hands On


## 90. AWS Snowball Edge - Pricing


## 91. Storage Gateway Overview


## 92. S3 Summary
