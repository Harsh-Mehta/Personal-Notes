# Amazon Simple Storage Service (S3)

## Introduction

* Amazon S3 is one of the main building blocks of AWS
* It’s advertised as ”infinitely scaling” storage
* Many websites use Amazon S3 as a backbone
* Many AWS services use Amazon S3 as an integration as well

## Use cases
* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application hosting
* Media hosting
* Data lakes & big data analytics
* Software delivery
* Static website

## Concepts

### Buckets
* Amazon S3 allows people to store objects (files) in “buckets” (directories)
* Buckets must have a globally unique name (across all regions all accounts)
* Buckets are defined at the region level
* S3 looks like a global service but buckets are created in a region
* Naming convention:
    * No uppercase
    * No underscore
    * 3-63 characters long
    * Not an IP
    * Must start with lowercase letter or number

### Objects
* Objects (files) have a Key
* The key is the FULL path:
    * s3://my-bucket/my_file.txt
    * s3://my-bucket/my\_folder1/another\_folder/my_file.txt
* The key is composed of prefix + object name
    * s3://my-bucket/my\_folder1/another\_folder/my\_file.txt
* There’s no concept of “directories” within buckets (although the UI will trick you to think otherwise)
* Just keys with very long names that contain slashes (“/”)
* Object values are the content of the body:
    * Max Object Size is 5TB (5000GB)
    * If uploading more than 5GB, must use “multi-part upload”
* Metadata (list of text key / value pairs – system or user metadata)
* Tags (Unicode key / value pair – up to 10) – useful for security / lifecycle
* Version ID (if versioning is enabled)

## Websites
* S3 can host static websites and have them accessible on the www
* The website URL will be:
    * \<bucket-name>.s3-website-\<AWS-region>.amazonaws.com OR
    * \<bucket-name>.s3-website.\<AWS-region>.amazonaws.com
* If you get a 403 (Forbidden) error, make sure the bucket policy allows public reads!

## Versioning
* One can version your files in Amazon S3
* It is enabled at the bucket level
* Same key overwrite will increment the “version”: 1, 2, 3….
* It is best practice to version your buckets
    * Protect against unintended deletes (ability to restore a version)
    * Easy roll back to previous version
* Notes:
    * Any file that is not versioned prior to enabling versioning will have version “null”
    * Suspending versioning does not delete the previous versions

## Access Logs
* For audit purpose, one may want to log all access to S3 buckets
* Any request made to S3, from any account, authorized or denied, will be logged into another S3 bucket
* That data can be analyzed using data analysis tools…
* Very helpful to come down to the root cause of an issue, or audit usage, view suspicious patterns, etc…

## Replication (CRR & SRR)
* Must enable versioning in source and destination
* Cross Region Replication (CRR)
* Same Region Replication (SRR)
* Buckets can be in different accounts
* Copying is asynchronous
* Must give proper IAM permissions to S3
* CRR - Use cases: compliance, lower latency access, replication across accounts
* SRR – Use cases: log aggregation, live replication between production and test accounts
