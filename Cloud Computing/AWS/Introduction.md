Amazon Web Services (AWS) owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web application.

# Pricing
* AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model
* Compute:
    * Pay for compute time
* Storage:
    * Pay for data stored in the Cloud
* Data transfer OUT of the Cloud:
    * Data transfer IN is free
* Solves the expensive issue of traditional IT

# Global Infrastructure
* AWS Regions
* AWS Availability Zones
* AWS Data Centers
* AWS Edge Locations/Points of Presence

## AWS Regions
* AWS has **Regions** all around the world
* Names can be us-east-1, eu-west-3…
* A region is a **cluster of data centers**
* Most AWS services are region-scoped

### How to choose an AWS Region?
* Compliance with data governance and legal requirements: data never leaves a region without your explicit permission
* Proximity to customers: reduced latency
* Available services within a Region: new services and new features aren’t available in every Region
* Pricing: pricing varies region to region and is transparent in the service pricing page

# Availability Zones
* Each region has many availability zones (usually 3, min is 2, max is 6). Example:
    * ap-southeast-2a
    * ap-southeast-2b
    * ap-southeast-2c
* Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity
* They’re separate from each other, so that they’re isolated from disasters
* They’re connected with high bandwidth, ultra-low latency networking

# Points of Presence
* Amazon has 216 Points of Presence (205 Edge Locations & 11 Regional Caches) in 84 cities across 42 countries
* Content is delivered to end users with lower latency

# AWS Services
* Some AWS services are global-scope:
    * Identity and Access Management (IAM)
    * Route 53 (DNS service)
    * CloudFront (Content Delivery Network)
    * WAF (Web Application Firewall)
* Most AWS services are region-scoped:
    * Amazon EC2 (Infrastructure as a Service)
    * Elastic Beanstalk (Platform as a Service)
    * Lambda (Function as a Service)
    * Rekognition (Software as a Service)

Region Table: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services

# AWS Shared Responsibility
![](../../assets/AWS_Shared_Responsibility_Model_V2.jpg)