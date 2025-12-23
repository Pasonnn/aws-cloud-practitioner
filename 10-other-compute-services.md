# Section 10: Other Compute Services: ECS, Lambda, Batch, Lightsail

## 112. What is Docker?

### What is Docker?

**Docker** is a software development platform to deploy apps using **containers**:

- **Apps are packaged in containers** that can be run on any OS
- **Apps run the same, regardless of where they're run**:
    - **Any machine** - your laptop, a server, the cloud
    - **No compatibility issues** - "it works on my machine" becomes "it works everywhere"
    - **Predictable behavior** - same environment everywhere
    - **Less work** - no need to configure environments manually
    - **Easier to maintain and deploy** - package once, run anywhere
    - **Works with any language, any OS, any technology**
- **Scale containers up and down very quickly** (seconds) - much faster than virtual machines

> Docker solves the "it works on my machine" problem by packaging applications with all their dependencies (libraries, runtime, system tools) into containers. A container is like a lightweight, portable box that contains everything your application needs to run. Unlike virtual machines which include a full operating system (taking up GBs of space and minutes to start), containers share the host's OS kernel and only include the application and its dependencies (taking up MBs and starting in seconds). This makes containers extremely portable - you can develop on your Mac, test on Linux, and deploy to AWS, and the application runs identically everywhere. Containers also enable microservices architecture - you can break a large application into small, independent services, each in its own container. This makes applications easier to develop, test, and scale. Docker has become the standard for containerization, and AWS provides several services (ECS, EKS, Fargate) to run Docker containers in the cloud.

### Docker on an OS
![Docker on an OS](assets/112-docker-on-an-os.png)

### Where Docker images are stored?
- Docker images are stored in Docker Repositories
- Public: Docker Hub https://hub.docker.com/
    - Find base images for many technologies or OS:
        - Ubuntu
        - MySQL
        - NodeJS, Java
- Private: Amazon ECR (Elastic Container Registry)

### Docker versus Virtual Machines

**Docker is "sort of" a virtualization technology, but not exactly**:

- **Resources are shared with the host** => many containers on one server
- Containers share the host OS kernel - more efficient
- Virtual Machines each have their own OS - more isolated but heavier

> The key difference between Docker containers and Virtual Machines is the level of virtualization. A Virtual Machine (VM) virtualizes the entire hardware - each VM gets virtualized CPU, RAM, disk, and network, plus a full operating system. This provides strong isolation (VMs are completely separate) but is resource-intensive - each VM needs its own OS, taking up GBs of RAM and disk space. Docker containers, on the other hand, virtualize at the operating system level - they share the host's OS kernel but have isolated user spaces. This makes containers much lighter (MBs instead of GBs) and faster to start (seconds instead of minutes). You can run many more containers on a server than VMs. However, containers are less isolated than VMs - they share the OS kernel, so a kernel vulnerability could potentially affect all containers. For most applications, containers provide the right balance of isolation, efficiency, and portability. Think of VMs like separate apartments (complete isolation, but each needs its own utilities), while containers are like rooms in a shared apartment (shared utilities, but each room is private).

![Docker versus Virtual Machines](assets/112-docker-vs-vm.png)

## 113. ECS, Fargate & ECR Overview

### ECS
- ECS = Elastic Container Service
- Launch Docker containers on AWS
- You must provision & maintain the infrastructure (the EC2 instances)
- AWS takes care of starting / stopping containers
- Has integrations with the Application Load Balancer

![ECS](assets/113-ecs.png)

### Fargate
- Launch Docker containers on AWS
- You do not provision the infrastructure (no EC2 instances to manage) - simpler!
- Serverless offering
- AWS just runs containers for you based on the CPU/RAM you need

![Fargate](assets/113-fargate.png)

### ECR
- Elastic Container Registry
- Private Docker Registry on AWS
- This is where you store your Docker images so they can be run by ECS or Fargate

![ECR](assets/113-ecr.png)

## 114. Amazon EKS

### Amazon EKS
- EKS = Elastic Kubernetes Service
- Allows you to launch managed Kubernetes clusters on AWS
- Kubernetes is an open-source system for management, deployment, and scaling of containerized apps (Docker)
- Containers can be hosted on:
    - EC2 instances
    - Fargate (Serverless)
- Kubernetes is cloud-agnostic (can be used in any cloud - Azure, GCP...)

![Amazon EKS](assets/114-amazon-eks.png)

## 115. Serverless Introduction

### What's Serverless?

**Serverless** is a new paradigm in which **developers don't have to manage servers anymore**:

- **They just deploy code** - no server configuration needed
- **They just deploy... functions!** - small units of code that run on demand
- **Initially... Serverless == FaaS (Function as a Service)**
- **Serverless was pioneered by AWS Lambda** but now also includes anything that's managed: "databases, messaging, storage, etc"
- **Serverless does not mean there are no servers**... it means you just don't manage / provision / see them

> Serverless is a misnomer - there are definitely servers involved, but you don't see or manage them. The cloud provider (AWS) handles all the server management, scaling, patching, and maintenance. You just write code and deploy it. AWS Lambda is the classic example - you write a function, upload it, and AWS runs it for you. You don't choose instance types, you don't configure servers, you don't worry about scaling. When your function is called, AWS automatically provisions the resources to run it, executes it, and then releases the resources. You only pay for the execution time. This is incredibly powerful for event-driven applications - like processing images when uploaded to S3, or responding to API requests. The serverless model has expanded beyond just functions - services like DynamoDB (serverless database), S3 (serverless storage), API Gateway (serverless API management) all follow the serverless model: you use them without managing infrastructure. The benefits are clear: no server management, automatic scaling, pay-per-use pricing, and faster time to market. However, serverless has limitations - functions have execution time limits, cold starts can cause latency, and debugging can be more challenging.

### So far in this course...

![Services](assets/115-services.png)

## 116. Lambda Overview

### Why AWS Lambda?

**Amazon EC2** (Traditional Approach):
- **Virtual Servers in the Cloud** - you manage the servers
- **Limited by RAM and CPU** - you choose the instance size
- **Continuously running** - you pay for the server even when idle
- **Scaling means intervention** to add / remove servers - manual or semi-automatic

**Amazon Lambda** (Serverless Approach):
- **Virtual functions - no servers to manage!** - AWS handles everything
- **Limited by time** - short executions (up to 15 minutes)
- **Run on-demand** - only runs when triggered
- **Scaling is automated!** - handles thousands of concurrent executions automatically

> Lambda represents a fundamental shift in how we think about compute. With EC2, you're renting a server - you pay for it 24/7, whether you're using it or not. With Lambda, you're renting execution time - you only pay when your code is actually running. This is like the difference between renting an apartment (EC2 - you pay monthly whether you're there or not) versus staying in a hotel (Lambda - you only pay for the nights you stay). Lambda automatically scales - if you get 1 request, Lambda runs 1 instance of your function. If you get 1000 requests simultaneously, Lambda automatically runs 1000 instances. You don't need to configure auto-scaling groups or load balancers. However, Lambda has constraints - functions can only run for up to 15 minutes, they have limited temporary storage, and there's a "cold start" delay (a few hundred milliseconds) when a function hasn't been used recently. Lambda is perfect for event-driven workloads - processing files uploaded to S3, responding to API requests, scheduled tasks, or reacting to database changes. For long-running processes or applications that need to stay "warm," EC2 might be more appropriate.

### Benefits of AWS Lambda
- Easy Pricing:
    - Pay per request and compute time
    - Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
- Integrated with the whole AWS suite of services
- Event-Driven: functions get invoked by AWS when needed
- Integrated with many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per functions (up to 10GB of RAM)
- Increasing RAM will also improve CPU and network!

### AWS Lambda language support
- Node.js (JavaScript)
- Python
- Java
- C# (.NET Core) / Powershell
- Ruby
- Custom Runtime API (community supported, example Rust or Golang)
- Lambda Container Image
    - The container image must implement the Lambda Runtime API
    - ECS / Fargate is preferred for running arbitrary Docker images

### Example: Serverless Thumbnail creation

![Example of Serverless Thumbnail Creation](assets/116-serverless-thumbnail-creation-example.png)

### Example: Serverless CRON Job

![Example of Serverless CRON Job](assets/116-cron-job-serverless-example.png)

### AWS Lambda Pricing: Example

**Lambda pricing** is based on two factors:

**Pay per calls**:
    - **First 1,000,000 requests are free** (per month, per account)
    - **$0.20 per 1 million requests thereafter** ($0.0000002 per request)

**Pay per duration** (in increments of 1 ms):
    - **400,000 GB-seconds of compute time per month is FREE**
    - This equals **400,000 seconds if function is 1 GB RAM**
    - This equals **3,200,000 seconds if function is 128 MB RAM**
    - After that **$1.00 for 600,000 GB-seconds**

**You can find overall pricing information here**: https://aws.amazon.com/lambda/pricing

**It is usually very cheap to run AWS Lambda** so it's very popular - perfect for sporadic workloads

> Lambda pricing is unique - you pay for two things: the number of times your function is invoked (requests) and how long it runs (duration × memory). The free tier is generous - 1 million free requests and 400,000 GB-seconds per month. For a function using 512 MB of RAM, that's about 800,000 seconds of free compute time (about 222 hours). This means many small applications can run entirely within the free tier. The pricing model makes Lambda extremely cost-effective for sporadic workloads - if your function runs once per day for 1 second, you're paying fractions of a cent. Compare this to EC2 where you'd pay for the instance 24/7 even if it's idle most of the time. However, for consistently high-traffic applications, EC2 might be cheaper due to the per-request and per-duration charges. The key is matching the pricing model to your workload - Lambda for sporadic, event-driven workloads; EC2 for consistent, always-on workloads.

## 117. Lambda Hands On
***This is a lab tutorial lesson***

## 118. API Gateway Overview

### Amazon API Gateway
- Example: building a serverless API
![Amazon API Gateway](assets/118-amazon-api-gateway.png)
- Fully managed service for developers to easily create, publishm maintain, monitor, and secure APIs
- Serverless and scalable
- Supports RESTful APIs and WebSocket APIs
- Support for security, user authentication, API throttling, API keys, monitoring...

## 119. Batch Overview

### AWS Batch
- Fully managed batch processing at any scale
- Efficiently run 100,000s of computing batch jobs on AWS
- A "batch" job is a job with a start and an end (opposed to continuous)
- Batch will dynamically launch EC2 instances or Spot Instances
- AWS Batch provisions the right amount of compute / memory
- You submit or schedule batch jobs and AWS Batch does the rest
- Helpful for cost optimizations and focusing less on the infrastructure

### AWS Batch - Simplified Example

![AWS Batch Simplified Example](assets/119-aws-batch-simplified-example.png)

### Batch vs Lambda

Understanding when to use **AWS Batch** versus **AWS Lambda**:

**Lambda**:
    - **Time limit** - functions can run for up to 15 minutes maximum
    - **Limited runtimes** - specific supported languages and versions
    - **Limited temporary disk space** - 512 MB to 10 GB ephemeral storage
    - **Serverless** - no infrastructure to manage

**Batch**:
    - **No time limit** - jobs can run for hours or days
    - **Any runtime** as long as it's packaged as a Docker image - complete flexibility
    - **Rely on EBS/instance store for disk space** - can use large amounts of storage
    - **Relies on EC2** (can be managed by AWS) - more control over the environment

> AWS Batch and Lambda serve different use cases. Lambda is perfect for short-running, event-driven tasks - processing a single image, handling an API request, or running a scheduled task that completes in seconds or minutes. Batch is designed for long-running, compute-intensive jobs - processing large datasets, running scientific simulations, rendering videos, or training machine learning models that might take hours or days. Think of Lambda as a quick errand (grab coffee) and Batch as a major project (renovate a house). Lambda has constraints (15-minute limit, limited storage) that make it unsuitable for large jobs. Batch can run any Docker container, so you have complete control over the environment, dependencies, and runtime. Batch automatically provisions the right EC2 instances (including Spot Instances for cost savings), runs your job, and cleans up when done. If you have a job that needs to process terabytes of data or run for several hours, Batch is the right choice. If you need to respond to an event in milliseconds and complete in seconds, Lambda is better.

## 120. Lightsail Overview

### Amazon Lightsail
- Virtual servers, storage, databases, and networking
- Low and predictable pricing
- Simpler alternative to using EC2, RDS, ELB, EBS, Route 53...
- Great for people with little cloud experience!
- Can setup notifications and monitoring of your Lightsail resources
- Use cases
    - Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js...)
    - Websites (templates for WordPress, Magento, Plesk, Joomla)
    - Dev / Test environment
- Has high availability but no auto-scaling, limited AWS integration

## 121. Lightsail Hands On
***This is a lab tutorial lesson***

## 122. Other Compute - Summary

### Other Compute - Summary
- Docker: container technology to run applications
- ECS: run Docker containers on EC2 instances
- Fargate:
    - Run Docker containers without provisioning the infrastructure
    - Serverless offering (no EC2 instances)
- ECR: Private Docker Images Repository
- Batch: run batch jobs on AWS across managed EC2 instances
- Lightsail: predictable and low pricing for simple application & DB stacks

### Lambda Summary
- Lambda is Serverless, Function as a Service, seamless scaling, reactive
- Lambda Billing:
    - By the time run x by the RAM provisioned
    - By the number of invocations
- Language Support: many programming languages except (arbitrary) Docker
- Invocation time: up to 15 minutes
- Use cases:
    - Create Thumbnails for images uploaded onto S3
    - Run a Serverless cron job
- API Gateway: expose Lambda functions as HTTP API
