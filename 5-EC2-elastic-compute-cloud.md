# Section 5: EC2 - Elastic Compute Cloud

## 34. AWS Budget Setup
***This is a lab tutorial lesson***

## 35. EC2 Basics

### Amazon EC2

**EC2** (Elastic Compute Cloud) is one of the most popular AWS offerings and represents **Infrastructure as a Service (IaaS)**.

**EC2** mainly consists of the capability to:

- **Renting virtual machines (EC2)** - servers in the cloud
- **Storing data on virtual drives (EBS)** - persistent block storage
- **Distributing load across machines (ELB)** - load balancing
- **Scaling the services using an auto-scaling group (ASG)** - automatic scaling

**Knowing EC2 is fundamental to understanding how the Cloud works** - it's the foundation of many AWS architectures.

### EC2 Sizing and Configuration Options

When launching an **EC2 instance**, you can configure various aspects:

- **Operating System (OS)**: Linux, Windows, or Mac OS
- **How much compute power and cores (CPU)**: Determines processing speed
- **How much random-access memory (RAM)**: Determines how much data can be processed simultaneously
- **How much storage space**:
    - **Network-attached (EBS & EFS)**: Persistent storage that survives instance termination
    - **Hardware (EC2 Instance Store)**: Temporary, high-performance storage attached directly to the instance
- **Network card**: Speed of the network card, **Public IP address** assignment
- **Firewall rules**: **Security group** - controls inbound and outbound traffic
- **Bootstrap script (configure at first launch)**: **EC2 User Data** - script that runs when the instance first starts

### EC2 User Data

**EC2 User Data** allows you to **bootstrap your instances** using a script:

- **Bootstrapping means launching commands when a machine starts** - automating initial setup
- **That script is only run once at the instance first start** - not on subsequent reboots
- **EC2 user data is used to automate boot tasks** such as:
    - **Installing updates** - keep the system current
    - **Installing software** - set up required applications
    - **Downloading common files from the internet** - fetch configuration files or data
    - **Anything you can think of** - any automation you need
- **The EC2 User Data Script runs with the root user** - has full administrative privileges

> EC2 User Data is like having a personal assistant set up your server automatically. Instead of manually logging into a new server and running commands to install software, configure settings, and download files, you write a script that does all of this automatically when the instance starts. This is incredibly powerful for automation - you can launch hundreds of identical servers, and they'll all configure themselves the same way. For example, you might use User Data to install a web server, download your application code from S3, configure the application, and start the service - all automatically. The script runs only once when the instance first boots, so it's perfect for initial setup. If you need to run commands on every boot, you'd use other methods like systemd services or cron jobs.

## 36. Create an EC2 Instance with EC2 User Data to have a Website Hands On

### Hands-On: Launching an EC2 Instance running Linux
- We'll be launching our first virtual server using the AWS Console
- We'll get a first high-level approach to the various parameters
- We'll see that our web server is launched using EC2 user data
- We'll learn how to start / stop / terminate our instance

***This is a lab tutorial lesson***

## 37. EC2 Instance Types Basics

### EC2 Instance Types - Overview

**You can use different types of EC2 instances** that are optimized for different use cases.

**AWS has the following naming convention**: `m5.2xlarge`

- **m**: Instance class (General Purpose, Compute Optimized, etc.)
- **5**: Generation (AWS improves them over time - newer generations are more efficient)
- **2xlarge**: Size within the instance class (nano, micro, small, medium, large, xlarge, 2xlarge, etc.)

**Instance Type Categories**:
- **General Purpose** - balanced compute, memory, and networking
- **Compute Optimized** - high-performance processors
- **Memory Optimized** - large amounts of RAM
- **Accelerated Computing** - hardware accelerators (GPUs, FPGAs)
- **Storage Optimized** - high, sequential read/write access to large datasets
- **HPC Optimized** - High Performance Computing workloads

### EC2 Instance Types - General Purpose

**General Purpose instances** are great for a diversity of workloads such as **web servers** or **code repositories**.

They provide a **balance between**:
    - **Compute** (CPU power)
    - **Memory** (RAM)
    - **Networking** (network performance)

**In this course, we will be using the `t2.micro`** which is a General Purpose EC2 instance and is eligible for the AWS Free Tier.

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

### Introduction to Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic allowed into or out of our EC2 Instances

![Inbound Outbound Traffic](assets/38-introduction-to-security-group.png)

- Security groups only contain allow rules
- Security groups rules can reference by IP or by security group

### Security Groups - Deeper Dive
- Security groups are acting as a "firewall"  on EC2 instances
- They regulate:
    - Access to Ports
    - Authorised IP ranges - IPv4 and IPv6
    - Control of inbound network (from other to the instance)
    - Control of outbound network (from the instance to other)

![Security Group Configuration](assets/38-security-groups.png)

### Security Groups Diagram

![Security Groups Diagram](assets/38-security-groups-diagram.png)

### Security Groups - Good to Know

Important facts about **Security Groups**:

- **Can be attached to multiple instances** - reuse the same security group across many instances
- **Locked down to a region / VPC combination** - security groups are specific to a region and VPC
- **Does live (outside) the EC2** - if traffic is blocked, the EC2 instance won't see it
    - Security groups act as a firewall before traffic reaches your instance
- **It is good to maintain one separate security group for SSH access** - makes it easier to manage SSH access separately
- **If your application is not accessible (time out)**, then it is likely a **security group issue** - traffic is being blocked
- **If your application gives a "connection refused" error**, then it's an **application error or it's not launched** - the security group is allowing traffic, but the application isn't responding
- **All inbound traffic is blocked by default** - you must explicitly allow inbound traffic
- **All outbound traffic is authorized by default** - instances can make outbound connections by default

> Understanding the difference between a timeout and "connection refused" is crucial for troubleshooting. A timeout means the security group is blocking the traffic - your request never reaches the instance. "Connection refused" means the traffic reached the instance (security group allowed it), but the application isn't listening on that port or isn't running. Think of it like a building: a timeout is like the security guard at the door stopping you (security group blocking), while "connection refused" is like reaching the office door but finding it locked (application not running or not listening on that port). Security groups are stateful - if you allow inbound traffic on a port, the corresponding outbound traffic is automatically allowed for responses.

### Referencing Other Security Groups Diagram
![Referencing Other Security Groups Diagram](assets/38-referencing-other-security-groups-diagram.png)

### Classic Ports to Know

Understanding common network ports is essential for configuring security groups:

- **22 = SSH (Secure Shell)** - log into a Linux instance
- **21 = FTP (File Transfer Protocol)** - upload files into a file share (less secure, rarely used)
- **22 = SFTP (Secure File Transfer Protocol)** - upload files using SSH (more secure than FTP)
- **80 = HTTP** - access unsecured websites (not encrypted)
- **443 = HTTPS** - access secured websites (encrypted with SSL/TLS)
- **3389 = RDP (Remote Desktop Protocol)** - log into a Windows instance

## 39. Security Groups Hands On
***This is a lab tutorial lesson***

## 40. SSH Overview

### SSH Summary Table
![SSH Summary Table](assets/40-ssh-summary-table.png)

### Which Lectures to Watch
- Mac / Linux:
    - SSH on Mac/Linux lecture
- Windows:
    - Putty Lecture
    - If Windows 10: SSH on Windows 10 lecture
- All:
    - EC2 Instance Connect lecture
### SSH troubleshooting
- Students have the most problems with SSH
- If things do not work...
    - 1. Re-watch the lecture. You may have missed something
    - 2. Read the troubleshooting guide
    - 3. Try EC2 Instance Connect
- If one method works (SSH, Putty or EC2 Instance Connect) you are good
- If no method works, that is okay, the course won't use SSH much

## 41. How to SSH using Linux or Mac

### How to SSH into your EC2 instance
- We will learn how to SSH into your EC2 instance using Linux / Mac
- SSH is one of the most important function. It allows you to control a remote machine, all using the command line

***This is a lab tutorial lesson***

> chmod 0400 key.pem
> ssh -i key.pem ec2-user@public.ip.v4.address

## 42. How to SSH using Windows
***This is a lab tutorial lesson***

## 43. How to SSH using Windows 10
***This is a lab tutorial lesson***

## 44. SSH Troubleshooting
***This is a lab tutorial lesson***

## 45. EC2 Instance Connect
***This is a lab tutorial lesson***

## 46. EC2 Instance Roles Demo
***This is a lab tutorial lesson***

## 47. EC2 Instance Purchasing Options

### EC2 Instances Purchasing Options
- On-Demand Instances - short workload, predictable pricing, pay by second
- Reserved (1 & 3 years)
    - Reserved Instances - long workloads
    - Convertible Reserved Instances - long workloads with flexible instances
- Savings Plans (1 & 3 years) - commitment to an amount of usage, long workload
- Spot Instances - short workloads, cheap, can lose instances (less reliable)
- Dedicated Hosts - book an entire physical server, control instance placement
- Dedicated Instances - no other customers will share your hardware
- Capacity Reservations - reserve capacity in a specific AZ for any duration

### EC2 On-Demand

**On-Demand Instances** are the most straightforward pricing model:

- **Pay for what you use**:
    - **Linux or Windows** - billing per second, after the first minute
    - **All other operating systems** - billing per hour
- **Has the highest cost** but **no upfront payment** - most flexible pricing
- **No long-term commitment** - start and stop anytime
- **Recommended for**:
    - Short-term and uninterrupted workloads
    - Applications where you can't predict how the application will behave
    - Testing and development
    - Applications with unpredictable workloads

### EC2 Reserved Instances

**Reserved Instances** provide significant cost savings for predictable workloads:

- **Up to 72% discount** compared to On-Demand pricing
- **You reserve specific instance attributes** (Instance Type, Region, Tenancy, OS)
- **Reservation Period**:
    - **1 year** (+ discount)
    - **3 years** (+++ discount) - highest savings
- **Payment Options**:
    - **No Upfront** (+) - pay monthly
    - **Partial Upfront** (++) - pay some upfront, rest monthly
    - **All Upfront** (+++) - pay everything upfront, highest discount
- **Reserved Instance's Scope**:
    - **Regional** - can be used across Availability Zones in a region
    - **Zonal** - reserve capacity in a specific Availability Zone
- **Recommended for steady-state usage applications** (think database, long-running applications)
- **You can buy and sell in the Reserved Instance Marketplace** - if your needs change
- **Convertible Reserved Instance**:
    - **Can change the EC2 instance type, instance family, OS, scope and tenancy**
    - **Up to 66% discount** - less discount but more flexibility

> Reserved Instances are like signing a lease for an apartment instead of paying daily hotel rates. If you know you'll need a server for at least a year, you can commit to that and get a significant discount. The longer the commitment (3 years vs 1 year) and the more you pay upfront (All Upfront vs No Upfront), the bigger the discount. However, you're locked into specific instance types and regions. Convertible Reserved Instances offer more flexibility - you can change instance types if your needs change - but with a smaller discount. Reserved Instances are perfect for production databases, web servers with steady traffic, or any application you know will run continuously for at least a year.

### EC2 Savings Plans

**Savings Plans** offer a more flexible alternative to Reserved Instances:

- **Get a discount based on long-term usage** (up to 72% - same as Reserved Instances)
- **Commit to a certain amount of usage** ($10/hour for 1 or 3 years)
- **Usage beyond EC2 Savings Plans is billed at the On-Demand price** - you're not locked to a specific instance
- **Locked to a specific instance family & AWS region** (e.g., M5 family in us-east-1)
- **Flexible across**:
    - **Instance Size** (e.g., m5.xlarge, m5.2xlarge) - can use any size in the family
    - **OS** (e.g., Linux, Windows) - can switch between operating systems
    - **Tenancy** (Host, Dedicated, Default) - can change tenancy models

> Savings Plans are like buying a monthly pass for public transportation instead of individual tickets. You commit to spending a certain amount per hour (e.g., $10/hour), and as long as you use instances from the same family (e.g., M5) in the same region, you get the discount. If you use more than your commitment, the excess is billed at On-Demand rates. The key advantage over Reserved Instances is flexibility - you can use any size instance (m5.small, m5.large, m5.xlarge) and switch between Linux and Windows, as long as they're in the M5 family. This is great if your workload varies in size but stays within the same instance family. For example, you might use m5.large during the day and m5.xlarge at night, and both count toward your Savings Plan commitment.

### EC2 Spot Instances

**Spot Instances** offer the **most cost-efficient** option in AWS, with up to **90% discount** compared to On-Demand:

- **Instances that you can "lose" at any point in time** if your max price is less than the current spot price
- **AWS can terminate your instance with a 2-minute warning** when they need the capacity
- **The MOST cost-efficient instances in AWS** - perfect for cost optimization
- **Useful for workloads that are resilient to failure**:
    - **Batch jobs** - data processing that can restart
    - **Data analysis** - analytical workloads that can be interrupted
    - **Image processing** - can reprocess if interrupted
    - **Any distributed workloads** - workloads that can handle node failures
    - **Workloads with a flexible start and end time** - not time-critical
- **Not suitable for critical jobs or databases** - cannot tolerate interruptions

> Spot Instances are like buying airline tickets at the last minute - you get a huge discount, but the airline can bump you if they need the seat. AWS has spare capacity that they're willing to sell at a discount, but if demand increases and someone is willing to pay more (or On-Demand customers need the capacity), AWS will terminate your Spot Instance with a 2-minute warning. This makes Spot Instances perfect for workloads that can handle interruptions - like processing a large dataset where if one instance dies, you can restart the job. However, they're terrible for databases or web servers that need to be always available. Many organizations use Spot Instances for 70-90% of their compute capacity, saving massive amounts of money, while keeping critical workloads on On-Demand or Reserved Instances.

### EC2 Dedicated Hosts
- A physical server with EC2 instance capacity fully dedicated to your use
- Allows you to address compliance requirements and use your existing server-bound software licenses (per-socket, per-core, pe-VM software licenses)
- Purchasing Options:
    - On-demand - pay per second for active Dedicated Host
    - Reserved - 1 or 3 years (No Upfront, Partial Upfront, All Upfront)
- The most expensive option
- Useful for software that have complicated licensing model (BYOL - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances run on hardware that's dedicated to you
- May share hardware with other instances in same account
- No control over instance placement (can move hardware after stop/start)

![Dedicated Instances and Dedicated Hosts Comparison](assets/47-dedicated-host-vs-instance.png)

### EC2 Capacity Reservations
- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- No time commitment (create/cancel anytime), no billing discount
- Combine with Regional Reserved Instances and Saving Plans to benefits from billing discount
- You're charged at On-Demand rate whether you run instances or not
- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ

### Which Purchasing Option is Right for Me?

Here's a helpful analogy using a resort hotel:

- **On-Demand**: Coming and staying in the resort whenever you like, you pay the full price
    - Most flexible, highest cost
    - Use for: unpredictable workloads, short-term needs

- **Reserved**: Like planning ahead - if you plan to stay for a long time, you may get a good discount
    - Commit to specific room type and duration
    - Use for: predictable, steady workloads (databases, production servers)

- **Savings Plans**: Pay a certain amount per hour for a certain period and stay in any room type (e.g., King, Suite, Sea View)
    - More flexible than Reserved, still get discounts
    - Use for: variable workloads within the same instance family

- **Spot Instances**: The hotel allows people to bid for empty rooms, and the highest bidder keeps the rooms. You can get kicked out at any time
    - Cheapest option, but can be interrupted
    - Use for: fault-tolerant, flexible workloads (batch processing, data analysis)

- **Dedicated Hosts**: You book an entire building of the resort
    - Most expensive, complete control
    - Use for: compliance requirements, software licensing needs

- **Capacity Reservations**: You book a room for a period with full price even if you do not stay in it
    - Guaranteed capacity, no discount
    - Use for: critical workloads that must run in a specific AZ

### Price Comparison - Example: m4.large - us-east-1
![Price Comparison of M4 Large in us-east-1](assets/47-price-comparison.png)

## 48. Shared Responsibility Model for EC2
![Shared Responsibility Model for EC2](assets/48-shared-responsibility-model-for-ec2.png)

## 49. EC2 Summary
- EC2 Instance: AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data
- Security Groups: Firewall attached to the EC2 instance
- EC2 User Data: Script launched at the first start of an instance
- SSH: start a terminal into our EC2 Instances (port 22)
- EC2 Instance Role: link to IAM roles
- Purchasing Options: On-Demand, Spot, Reserved (Standard + Convertible), Dedicated Host, Dedicated Instance
