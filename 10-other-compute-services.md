# Section 10: Other Compute Services: ECS, Lambda, Batch, Lightsail

## 112. What is Docker?

### What is Docker?
- Docker is a software development platform to deploy apps
- Apps are packaged in containers that can be run on any OS
- Apps run the same, regardless of where they're run
    - Any machine
    - No compatibility issues
    - Predictable behavior
    - Less work
    - Easier to maintain and deploy
    - Works with any language, any OS, any technology
- Scale containers up and down very quickly (seconds)

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
- Docker is "sort of" a virtualization technology, but not exactly
- Resources are shared with the host => many containers on one server

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

### What's serverless?
- Serverless is a new paradigm in which the developers don't have to manage servers anymore...
- They just deploy code
- They just deploy... functions!
- Initially... Serverless == FaaS (Function as a Service)
- Serverless was pioneered by AWS Lambda but now also includes anything that's managed: "databases, messaging, storage, etc"
- Serverless does not mean there are no servers... it means you just don't manage / provision / see them

### So far in this course...

![Services](assets/115-services.png)

## 116. Lambda Overview

### Why AWS Lambda

**Amazon EC2**
-

## 117. Lambda Hands On

## 118. API Gateway Overview

## 119. Batch Overview

## 120. Lightsail Overview

## 121. Lightsail Hands On

## 122. Other Compute - Summary
