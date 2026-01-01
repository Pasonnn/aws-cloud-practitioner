# Section 15: VPC & Networking

## 171. VPC Overview

### VPC - Crash Course
- VPC is something you should know in depth for the AWS Certified Solutions Architect Associate & AWS Certified SysOps Administrator
- At the AWS Certified Cloud Practitioner Level, you should know about:
    - VPC, Subnets, Internet Gateways & NAT Gateways
    - Security Groups, Network ACL (NACL), VPC Flow Logs
    - VPC Peering, VPC Endpoints
    - Site to Site VPN & Direct Connect
    - Transit Gateway
- I will just give you an overview, less than 1 or 2 questions at your exam
- We will have a look at the "default VPC" (created by default by AWS for you)
- There is a summary lecture at the end. It's play if you don't understand it all

## 172. IP Addresses in AWS

### IP Addresses in AWS
- IPv4 - Internet Protocol version 4 (4.3 billion addresses)
    - Public IPv4 - can be used on the Internet
    - EC2 instance gets a new a public IP address everytime yous top then start it (default)
    - Private IPv4 - can be used on private networks (LAN) such as internal AWS networking (e.g., 192.168.1.1)
    - Elastic IP - allows you to attach a fixed public IPv4 address to EC2 instance
    - Note: all public IPv4 on AWS will be charge $0.005 per hour (including EIP)
    - IPv6 - Internet Protocol version 7 (3.4 x 10^38 addresses)
        - Every IP address is public in AWS (no private range)
        - Example: 2001:db8:3333:4444:cccc:dddd:eeee:ffff
        - Free

## 173. VPC, Subnet, Internet Gateway & NAT Gateways

### VPC & Subnets Primer
- VPC - Virtual Private Cloud: private network to deploy your resources (regional resource)
- Subnets allow you to partition your network inside you VPC (Availability Zone resource)
- A public subnet is a subnet that is accessible from the internet
- To define access to the internet and between subnets, we use Route Tables

![VPC and Subnets Primer](assets/173-vpc-subnets-primer.png)

### VPC Diagram

![VPC Diagram](assets/173-vpc-diagram.png)

### Internet Gateway & NAT Gateways

- Internet Gateways helps our VPC instances connect with the internet
- Public Subnets have a route to the internet gateway
- NAT Gateways (AWS-managed) & NAT Instances (self-managed) allow your instances in your Private Subnets to access the internet while remaining private

![Internet Gateway and NAT Gateways](assets/173-internet-gateway-nat-gateways.png)

## 174. VPC, Subnet, Internet Gateway & NAT Gateways - Hands On
***This is a lab tutorial lesson***

## 175. Security Groups & Network Access Control List (NACL)

- NACL (Network ACL)
    - A firewall which controls traffic from and to subnet
    - Can have ALLOW and DENY rules
    - Are attached at the Subnet level
    - Rules only include IP addresses
- Security Groups
    - A firewall that controls traffic to and from an EC2 Instance
    - Can have only ALLOW rules
    - Rules include IP addresses and other security groups

![Network ACL and Security Groups](assets/175-network-acl-and-security-groups.png)

### Network ACLs vs Security Groups

| Security Group | Network ACL |
| -------------- | ----------- |
| Operates at the instance level | Operates at the subnet level |
| Supports allow rules only | Supports allow rules and deny rules |
| Is stateful: Return traffic is automatically allowed, regardless of any rules | Is stateless: Return traffic must be explicitly allowed by rules |
| We evaluate all rules before deciding whether to allow traffic | We process rules in number order when deciding whether to allow traffic |
| Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance later on | Automatically applies to all instances in the subnets it's associated with (therefore, you don't have to rely on users to specify the security group) |

### Hands On
***This is a lab tutorial lesson***

## 176. VPC Flow Logs & VPC Peering

### VPC Flow Logs
- Capture information about IP traffic going into your interfaces:
    - VPC Flow Logs
    - Subnet Flow Logs
    - Elastic Network Interface Flow Logs
- Helps to monitor and troubleshoot connectivity issues. Example:
    - Subnets to internet
    - Subnets to subnets
    - Internet to subnets
- Captures network information from AWS managed interfaces too: Elastic Load Balancers, ElasticCache, RDS, Aurora, etc...
- VPC Flow logs data can go to S3, CloudWatch Logs, and Amazon Data Firehose

### VPC Peering
- Connect two VPC, privately using AWS' network
- Make then behave as if they were in the same network
- Must not have overlapping CIDR (IP address range)
- VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another)

![VPC Peering](assets/176-vpc-peering.png)

### Hands On
***This is a lab tutorial lesson***

## 177. VPC Endpoints - Interface & Gateway (S3 & DynamoDB)

## 178. PrivateLink

## 179. Direct Connect & Site-to-Site VPN

## 180. Client VPN

## 181. Transit Gateway Overview

## 182. VPC & Networking Summary
