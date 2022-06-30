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
