# Section 3: What is Cloud Computing

## 7. Traditional IT Overview

### How websites work

Client - Network - Server

- Clients have IP addresses
- Servers have IP addresses

### What is a server composed of?

- Compute: CPI
- Memory: RAM
- Storage: Data
- Database: Store data in a structured way
- Network: Routers, switch, DNS server

### IT Terminology
- Network: cables, routers and servers connected with each other
- Router: A networking device that forwards data packets between computer networks. They know where to send your packets on the internet
- Switch: Takes a packet and send it to the correct server / client on your network

![IT Terminology](assets/it-terminology.png)

### Traditionally, how to build infrastructure
- Data store in Home or Garage
- Move to Office and have a Data center

### Problems with traditional IT approach
- Pay for the rent for the data center
- Pay for power supply, cooling, maintenance
- Adding and replacing hardware takes time
- Scaling is limited
- Hire 24/7 team to monitor the infrastructure
- How to deal with disasters?
- Can we externalize all this?

## 8. What is Cloud Computing

### What is Cloud Computing
- Cloud computing is the on-demand delivery of compute power, database storage, applications, and other IT resources
- Through a cloud services platform with pay-as-you-go pricing
- You can provision exactly the right type and size of computing resources you need
- You can access as many resources as you need, almost instantly
- Simple way to access servers, storage, databases and a set of application services

&rarr; Amazon Web Services owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web application

### You have been using some Cloud services
- Gmail:
    - E-mail cloud service
    - Pay for ONLY your emails stored (no infrastructure, etc.)
- Dropbox:
    - Cloud Storage Service
    - Originally built on AWS
- Netflix:
    - Built on AWS
    - Video on Demand

### The Depoyment Models of the Cloud
- Private Cloud:
    - Cloud services used by a single organization, not exposed to the public
    - Complete control
    - Security for sensitive applications
    - Meet specific business needs
- Public Cloud:
    - Cloud resources owned and operated by a third-party cloud service provider delivered over the Internet
    - Six Advanages of Cloud Computing
- Hybrid Cloud:
    - Keep some servers on premises and extend some capabilities to the Cloud

### The Five Characteristics of Cloud Computing
- On-demand self service:
    - Users can provision resources and use them without human interaction from the service provider
- Broad network access:
    - Resources available over the network, and can be accessed by diverse client platforms
- Multi-tenancy and resource pooling:
    - Multiple customers can share the same infrastructure and applications with security and privacy
    - Multiple customers are services from the same physical resources
- Rapid elasticity and scalability:
    - Automatically and quickly acquire and disponse resources when needed
    - Quickly and easily scale based on demand
- Measured service:
    - Usage is measured, users pay correctly for what they have used

### Six Advantages of Cloud Computing
- Trade capital expense (CAPEX) for operational expense (OPEX)
    - Pay On-Demand: don't own hardware
    - Reduced Total Cost of Ownership (TCO) & Operational Expense (OPEX)
- Benefit from massiv economies of scale
    - Prices are reduced as AWS is more efficient due to large scale
- Stop guessing capacity
    - Scale based on actual measured usage
- Increase speed and agility
- Stop spending money running and maintaining data centers
- Go global in minuted: leverage the AWS global infrastructure

### Problems solved by the Cloud
- Flexibility: change resource types when needed
- Cost-Effectiveness: pay as you go, for what you need
- Scalability: accommodate larger loads by making hardware stronger or adding additional nodes
- Elasticity: ability to scale out and scale-in when needed
- High-availablility and fault-tolerance: built across data centers
- Agility: rapidly develop, test and launch software applications

## 9. The Different Types of Cloud Computing

### Types of Cloud Computing
- Infrastructure as a Service (IaaS)
    - Provide building blocks for cloud IT
    - Provide networking, computers, data storage space
    - Highest level of flexibiltiy
    - Easy parallel with traditional on-premises IT
- Platform as a Service (PaaS)
    - Removes the need for your organization to manage the underlying infrastructure
    - Focus on the deployment and management of your application
- Software as a Service (SaaS)
    - Completed product that is run and managed by the service provider

![Types of Cloud Computing Responsibility](assets/9-types-of-cloud-compare.png)

### Example of Cloud Computing Types

- Infrastructure as a Service:
    - Amazon EC2 (on AWS)
    - GCP, Azure, Rackspace, Digital OCean, Linode
- Platform as a Service:
    - Elastic Beanstalk (on AWS)
    - Heroky, Google App Enginer (GCP), Window Azure (Microsoft)
- Software as a Service:
    - Many AWS services (ex: Rekognition for Machine Learning)
    - Google Apps (Gmail), Dropbox, Zoom

### Prixing of the Cloud - Quick Overview
- AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model
- Compute:
    - Pay for compute time
- Storage:
    - Pay for data stored in the Cloud
- Data transfer OUT of the Cloud:
    - Data transfer IN is free
- Solved the expensive issue of traditional IT

## 10. AWS Cloud Overview

### AWS Cloud History

- 2002: Internally launched
- 2003: Amazon infrastructure is one of their core strength, Idea to market
- 2004: Launched publicly with SQS
- 2006: Re-launched publicly with SQS, S3 & EC2
- 2007: Launched in Europe

### AWS Cloud Number Facts

- In 2023, AWS had $90 billion in annual revenue
- AWS accounts for 31% of the market in Q1 2024 (Microsoft is 2nd with 25%)
- Pioneer and Leader of the AWS Cloud Market for the 13th consecutive year
- Over 1,000,000 active users

### AWS Cloud Use Cases

- AWS enables you to build sophisticated, scalable applications
- Applicable to a diverse set of industries
- Use cases include:
    - Enterprise IT, Backup & Storage, Big Data analytics
    - Website hosting, Mobile and Social Apps
    - Gaming

### AWS Global Infrastructure
- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations / Points of Presence

### AWS Regions
- AWS has Regions all around the world
- Names can be us-east-1, eu-west-3, etc
- A region is a cluster of data centers
- Most AWS services are region-scoped

### How to choose an AWS Region
***If you need to launch a new application where should you do it?
***
- Compliance with data governance and legal requirements: data never leaves a region without your explicit permission
- Proximity services within a Region: new services and new features aren't available in every Region
- Pricing: pricing varies region to region and is transparent in the service pricing page

### AWS Availability Zones
- Each region as many availability zones (usually 3, min is 3, max is 6). Example:
    - ap-southeast-2a
    - ap-southeast-2b
    - ap-southeast-2c
- Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity
- They are separate from each other, so that they are isolated from disasters
- They are connected with high bandwidth, ultra-low latancy networking

![AWS Region](assets/10-aws-region.png)

### AWS Points of Presence (Edge Locations)
- Amazon has 400+ Points of Presence (400+ Edge Locations & 10+ Regional Caches) in 90+ cities across 40+ countries
- Content is delivered to end users with lower latency

### Tour of the AWS Console
- AWS has Global Services:
    - Identity and Access Management (IAM)
    - Route 53 (DNS Service)
    - CloudFront (Content Delivery Network)
    - WAF (Web Application Firewall)
- Most AWS services are Region-scoped:
    - Amazon EC2 (Infrastructure as a Service)
    - Elastic Beanstalk (Platform as a Service)
    - Lambda (Function as a Service)
    - Rekognition (Software as a Service)
