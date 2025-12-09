# Section 5: EC2 - Elastic Compute Cloud

## 34. AWS Budget Setup
***This is a lab tutorial lesson***

## 35. EC2 Basics

### Amazon EC2
- EC2 is one of the most popular of AWS' offering
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly cosists in the capability of:
    - Renting virtual machines (EC2)
    - Storing data on virtual drives (EBS)
    - Distributing load across machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)
- Knowing EC2 is fundamental to understand how the Cloud works

### EC2 sizing and configuration options
- Operating System (OS): Linux, Windows or Mac OS
- How much compute power and cores (CPU)
- How much random-access memory (RAM)
- How much storage space:
    - Network-attached (EBS & EFS)
    - Hardware (EC2 Instance Store)
- Network card: speed of the card, Public IP address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 User Data

### EC2 User Data
- It is possible to bootstap our instances using an EC2 User Data script
- Bootstrapping means launching commands when a machine starts
- That script is only run one at the instance first start
- EC2 user data is used to automate boot tasks such as:
    - Installing updates
    - Installing software
    - Downloading common files from the internet
    - Anything you can thing of
- The EC2 User Data Script runs with the root user

## 36. Create an EC2 Instance with EC2 User Data to have a Website Hands On

### Hands-On: Launching an EC2 Instance running Linux
- We'll be launching our first virtual server using the AWS Console
- We'll get a first high-level approach to the various parameters
- We'll see that our web server is launched using EC2 user data
- We'll learn how to start / stop / terminate our instance

***This is a lab tutorial lesson***

## 37. EC2 Instance Types Basics

### EC2 Instance Types - Overview
- You can use different types of EC2 instances that are optimized for different use cases
- AWS has the following naming convention: m5.2xlarge
    - m: instance class
    - 5: generation (AWS improves them over time)
    - 2xlargeL size within the instance class
- General Purpose, Compute Optimized, Memory Optimized, Accelerated Computing, Storage Optmized, HPC Optimized, Instance Features, Measuring Instance Performance

### EC2 Instance Types - General Purpose
- Great for a diversity of workloads such as web servers or code repositories
- Balance between:
    - Compute
    - Memory
    - Networking
- In the course, we will be using the t2.micro which is a General Purpose EC2 isntance

### EC2 Instance Types - Compute Optimized
- Great for compute-intensive tasks that require high performance processors:
    - Batch processing workloads
    - Media transcoding
    - High performance web servers
    - High performance computing (HPC)
    - Scientific modeling and machine learning
    - Dedicated gaming servers

### EC2 Instance Types - Memory Optmized
- Fast performance for workloads that process large data sets in memory
- Use cases:
    - High performance, relational/non-relational databases
    - Distributed web scale cache stores
    - In-memory databases optimized for BI (business intelligence)
    - Applications performing real-time processing of big unstructured data

### EC2 Instance Types - Storage Optimized
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
    - High frequency online transaction processing (OLTP) systems
    - Relational and NoSQL databases
    - Cache for in-memory databases (for example, Redis)
    - Data warehousing applications
    - Distributed file systems

### EC2 Instance Types: Example
![EC2 Instance Types Example](assets/37-ec2-instance-types.png)

## 38. Security Groups & Classic Ports Overview



## 39. Security Groups Hands On

## 40. SSH Overview

## 41. How to SSH using Linux or Mac

## 42. How to SSH using Windows

## 43. How to SSH using Windows 10

## 44. SSH Troubleshooting

## 45. EC2 Instance Connect

## 46. EC2 Instance Roles Demo

## 47. EC2 Instance Purchasing Options

## 48. Shared Responsibility Model for EC2

## 49. EC2 Summary
