# Introduction
* Amazon Elastic Compute Cloud (Amazon EC2) is an AWS service that offers a compute platform with a gigantic choice of the latest processor, storage, networking, operating system to match the workload requirements.
* It is one of the most popular of AWS’ offering
* EC2 = Elastic Compute Cloud = Infrastructure as a Service
* It mainly consists in the capability of :
    * Renting virtual machines (EC2)
    * Storing data on virtual drives (EBS)
    * Distributing load across machines (ELB)
    * Scaling the services using an auto-scaling group (ASG)
* Knowing EC2 is fundamental to understand how the Cloud works

# EC2 Sizing & configuration options
* Operating System (OS): Linux, Windows or Mac OS
* How much compute power & cores (CPU)
* How much random-access memory (RAM)
* How much storage space:
    * Network-attached (EBS & EFS)
    * hardware (EC2 Instance Store)
* Network card: speed of the card, Public IP address
* Firewall rules: security group
* Bootstrap script (configure at first launch): EC2 User Data

# EC2 User Data
* It is possible to bootstrap our instances using an EC2 User data script.
* bootstrapping means launching commands when a machine starts
* That script is only run once at the instance first start
* EC2 user data is used to automate boot tasks such as:
    * Installing updates
    * Installing software
    * Downloading common files from the internet
    * Anything you can think of
* The EC2 User Data Script runs with the root user

# EC2 Instance Types
* There are different types of EC2 instances that are optimised for different use cases (https://aws.amazon.com/ec2/instance-types/) and the following are a few:
    * General Purpose:
        * Great for a diversity of workloads such as web servers or code repositories
        * Balance between:
            * Compute
            * Memory
            * Networking
    * Compute Optimized
        * Great for compute-intensive tasks that require high performance processors:
            * Batch processing workloads
            * Media transcoding
            * High performance web servers
            * High performance computing (HPC)
            * Scientific modeling & machine learning
            * Dedicated gaming servers
    * Memory Optimized
        * Fast performance for workloads that process large data sets in memory
        * Use cases:
            * High performance, relational/non-relational databases
            * Distributed web scale cache stores
            * In-memory databases optimized for BI (business intelligence)
            * Applications performing real-time processing of big unstructured data
    * Storage Optimized
        * Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
        * Use cases:
            * High frequency online transaction processing (OLTP) systems
            * Relational & NoSQL databases
            * Cache for in-memory databases (for example, Redis)
            * Data warehousing applications
            * Distributed file systems
* AWS has the following naming convention:

    > m5.2xlarge

    Where,
    * **m:** instance class
    * **5:** generation (AWS improves them over time)
    * **2xlarge:** size within the instance class

# EC2 Security groups
* Security Groups are the fundamental of network security in AWS
* They control how traffic is allowed into or out of our EC2 Instances.
* Security groups only contain allow rules
* Security groups rules can be referenced by IP or by security group
* Security groups acts as a “firewall” on EC2 instances
* They regulate:
    * Access to Ports
    * Authorised IP ranges – IPv4 and IPv6
    * Control of inbound network (from other to the instance)
    * Control of outbound network (from the instance to other)

## Good to know
* Can be attached to multiple instances
* Locked down to a region / VPC combination
* Does live “outside” the EC2 – if traffic is blocked the EC2 instance won’t see it
* It’s good to maintain one separate security group for SSH access
* If the application is not accessible (time out), then it’s a security group issue
* If the application gives a “connection refused“ error, then it’s an application error or it’s not launched
* All inbound traffic is blocked by default
* All outbound traffic is authorised by default

# Important Ports
* 22 = SSH (Secure Shell) - log into a Linux instance
* 21 = FTP (File Transfer Protocol) – upload files into a file share
* 22 = SFTP (Secure File Transfer Protocol) – upload files using SSH
* 80 = HTTP – access unsecured websites
* 443 = HTTPS – access secured websites
* 3389 = RDP (Remote Desktop Protocol) – log into a Windows instance

# Secure-Shell (SSH) summary table
| OS            | SSH  | PuTTY  | EC2 Instance Connect  |
|---------------|------|--------|-----------------------|
| Mac           | Yes  | No     | Yes                   |
| Linux         | Yes  | No     | Yes                   |
| Windows < 10  | No   | Yes    | Yes                   |
| Windows > =10 | Yes  | Yes    | Yes                   |

# EC2 Instance Connect
* Connect to your EC2 instance within your browser
* No need to use your key file that was downloaded
* The “magic” is that a temporary key is uploaded onto EC2 by AWS
* Works only out-of-the-box with Amazon Linux 2
* Need to make sure the port 22 is still opened!

# EC2 Instances Purchasing Options
* On-Demand Instances – short workload, predictable pricing, pay by second
* Reserved (1 & 3 years)
    * Reserved Instances – long workloads
    * Convertible Reserved Instances – long workloads with flexible instances
* Savings Plans (1 & 3 years) –commitment to an amount of usage, long workload
* Spot Instances – short workloads, cheap, can lose instances (less reliable)
* Dedicated Hosts – book an entire physical server, control instance placement
* Dedicated Instances – no other customers will share your hardware
* Capacity Reservations – reserve capacity in a specific AZ for any duration

## On Demand Instances
* Pay for what you use:
    * Linux or Windows - billing per second, after the first minute
    * All other operating systems - billing per hour
* Has the highest cost but no upfront payment
* No long-term commitment
* Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave

## Reserved Instances
* Up to 72% discount compared to On-demand
* You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
* Reservation Period – 1 year (+discount) or 3 years (+++discount)
* Payment Options – No Upfront (+), Partial Upfront (++), All Upfront (+++)
* Reserved Instance’s Scope – Regional or Zonal (reserve capacity in an AZ)
* Recommended for steady-state usage applications (think database)
* You can buy and sell in the Reserved Instance Marketplace
* Convertible Reserved Instance
    * Can change the EC2 instance type, instance family, OS, scope and tenancy
    * Up to 66% discount

**NOTE:** the % discounts are subject to change as AWS may keep changing it over time

## Savings Plans
* Get a discount based on long-term usage (up to 72% - same as RIs)
* Commit to a certain type of usage ($10/hour for 1 or 3 years)
* Usage beyond EC2 Savings Plans is billed at the On-Demand price
* Locked to a specific instance family & AWS region (e.g., M5 in us-east-1)
* Flexible across:
    * Instance Size (e.g., m5.xlarge, m5.2xlarge)
    * OS (e.g., Linux, Windows)
    * Tenancy (Host, Dedicated, Default)

## Spot Instances
* Can get a discount of up to 90% compared to On-demand
* Instances that you can “lose” at any point of time if your max price is less than the
current spot price
* The MOST cost-efficient instances in AWS
* Useful for workloads that are resilient to failure
    * Batch jobs
    * Data analysis
    * Image processing
    * Any distributed workloads
    * Workloads with a flexible start and end time
* Not suitable for critical jobs or databases

## Dedicated Hosts
* A physical server with EC2 instance capacity fully dedicated to your use
* Allows you address compliance requirements and use your existing serverbound software licenses (per-socket, per-core, per—VM software licenses)
* Purchasing Options:
    * On-demand – pay per second for active Dedicated Host
    * Reserved - 1 or 3 years (No Upfront, Partial Upfront, All Upfront)
* The most expensive option
* Useful for software that have complicated licensing model (BYOL – Bring Your Own License)
* Or for companies that have strong regulatory or compliance needs

## EC2 Dedicated Instances
* Instances run on hardware that’s dedicated to you
* May share hardware with other instances in same account
* No control over instance placement (can move hardware after Stop / Start)

### Dedicated Instances vs Dedicated Hosts
+-------------------------------------------------------+-----------------+---------------------+
| Characteristic                                        | Dedicated Hosts | Dedicated Instances |
+=======================================================+=================+=====================+
| Enables the use of dedicated physical servers         | Yes             | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Per instance billing (subject to a $2 per region fee) | No              | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Per host billing                                      | Yes             | No                  |
+-------------------------------------------------------+-----------------+---------------------+
| Visibility of sockets, cores, host ID                 | No              | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Affinity between a host and instance                  | No              | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Targeted instance placement                           | No              | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Automatic instance placement                          | Yes             | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+
| Add capacity using an allocation request              | No              | Yes                 |
+-------------------------------------------------------+-----------------+---------------------+

## EC2 Capacity Reservations
* Reserve On-Demand instances capacity in a specific AZ for any duration
* You always have access to EC2 capacity when you need it
* No time commitment (create/cancel anytime), no billing discounts
* Combine with Regional Reserved Instances and Savings Plans to benefit from billing discounts
* You’re charged at On-Demand rate whether you run instances or not
* Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ

# Selecting the right purchasing option
* On demand: coming and staying in resort whenever we like, we pay the full price
* Reserved: like planning ahead and if we plan to stay for a long time, we may get a good discount.
* Savings Plans: pay a certain amount per hour for certain period and stay in any room type (e.g., King, Suite, Sea View, …)
* Spot instances: the hotel allows people to bid for the empty rooms and the highest bidder keeps the rooms. You can get kicked out at any time
* Dedicated Hosts: We book an entire building of the resort
* Capacity Reservations: you book a room for a period with full price even you don’t stay in it

# Shared Responsibility Model for EC2
+-------------------------------+------------------------------------+
| AWS                           | User                               |
+===============================+====================================+
| * Infrastructure (global      | * Security Groups rules            |
| network security)             | * Operating-system patches and     |
| * Isolation on physical hosts | updates                            |
| * Replacing faulty hardware   | * Software and utilities installed |
| * Compliance validation       | on the EC2 instance                |
|                               | * IAM Roles assigned to EC2 &      |
|                               | IAM user access management         |
|                               | * Data security on your instance   |
+-------------------------------+------------------------------------+

# Summary
* EC2 Instance: AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data
* Security Groups: Firewall attached to the EC2 instance
* EC2 User Data: Script launched at the first start of an instance
* SSH: start a terminal into our EC2 Instances (port 22)
* EC2 Instance Role: link to IAM roles
* Purchasing Options: On-Demand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance