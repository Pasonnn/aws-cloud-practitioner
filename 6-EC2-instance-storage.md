# Section 6: EC2 Instance Storage

## 50. EBS Overview

### What's an EBS Volume?
- An EBS (Elastic Block Store) Volume is network drive you can attach to your instances while they run
- It allows your instances to persist data, even after their termination
- They can only be mounted to one instance at a time (at a CCP level)
- They are bound to a specific availability zone
- Analogy: Think of them as a "network USB stick"

### EBS Volume
- It's a network drive (i.e. not a physical drive)
    - It uses the network to communicate the instance, which means there might be a bit of latency
    - It can be detached from an EC2 instance and attached to another one quickly
- It's locked to an Availability Zone (AZ)
    - An EBS Volume in us-east-1a cannot be attached to us-east-1b
    - To move a volume across, you first need to snapshot it
- Have a provisioned capacity (size in GBs, and IOPS)
    - You get billed for all the provisioned capacity
    - You can increase the capacity of the drive over time

### EBS Volume - Example
![Example of EBS Volume](assets/50-example-of-ebs-volume.png)

### EBS - Delete on Termination Attribute

![EBS Terminal Attribute Delete](assets/50-terminal-attribute-delete.png)

## 51. About EBS Multi-Attach


## 52. EBS Hands On


## 53. EBS Snapshots Overview


## 54. EBS Snapshots Hands On


## 55. AMI Overview


## 56. AMI Hands On


## 57. EC2 Image Builder Overview


## 58. EC2 Instance Store


## 59. EFS Overview


## 60. Shared Responsibility Model for EC2 Storage


## 61. Amazon FSx Overview


## 62. EC2 Instance Storage Summary


## 63. Section Cleanup
