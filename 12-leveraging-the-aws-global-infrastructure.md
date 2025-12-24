# Section 12: Leveraging the AWS Global Infrastructure

## 138. Why Global Applications?

### Why Make a Global Application?

A **global application** is an application deployed in multiple geographies. On AWS, this could be **Regions** and/or **Edge Locations**.

**Key reasons to go global**:

1. **Decreased Latency**
    - **Latency is the time it takes for a network packet to reach a server**
    - **It takes time for a packet from Asia to reach the US** - physical distance creates delay
    - **Deploy your applications closer to your users** to decrease latency and provide a better experience

2. **Disaster Recovery (DR)**
    - **If an AWS region goes down** (earthquake, storms, power shutdown, politics)...
    - **You can fail-over to another region** and maintain service availability
    - **A DR plan is important to increase the availability** of your application

3. **Attack Protection**
    - **Distributed global infrastructure is harder to attack** - spreading resources makes them more resilient

> Going global isn't just about having users in different countries - it's about providing the best possible experience and ensuring your application stays online even when things go wrong. Latency is a critical factor - if a user in Tokyo has to wait 200 milliseconds for each page load because your servers are in Virginia, that's a poor experience. By deploying closer to users (in the Asia-Pacific region), you can reduce that latency to 20-30 milliseconds. Disaster recovery is equally important - if an entire AWS region fails (which is rare but possible due to natural disasters, power outages, or other catastrophic events), having your application running in another region means you can failover and continue serving users. This is called "multi-region" deployment. Additionally, distributing your infrastructure globally makes it harder for attackers to take down your entire service - they'd have to attack multiple regions simultaneously. Global applications are essential for businesses that serve customers worldwide and need high availability.

### Global AWS Infrastructure

AWS provides a global infrastructure with three main components:

- **Regions**: For deploying applications and infrastructure - full AWS services in specific geographic areas
- **Availability Zones**: Made of multiple data centers - isolated locations within regions for high availability
- **Edge Locations (Points of Presence)**: For content delivery as close as possible to users - caches and content delivery points

**More information at**: https://infrastructure.aws/

### Global Applications in AWS

AWS provides several services to help you build and operate global applications:

- **Global DNS: Route 53**
    - **Great to route users to the closest deployment** with least latency
    - **Great for disaster recovery strategies** - automatic failover between regions

- **Global Content Delivery Network (CDN): CloudFront**
    - **Replicate part of your application to AWS Edge Locations** - decrease latency
    - **Cache common requests** - improved user experience and decreased latency

- **S3 Transfer Acceleration**
    - **Accelerate global uploads & downloads** into Amazon S3
    - Uses CloudFront's edge network to optimize transfers

- **AWS Global Accelerator**
    - **Improve global application availability and performance** using the AWS global network
    - Provides static IP addresses and intelligent routing

## 139. Route 53 Overview

### Amazon Route 53 Overview

**Route 53** is a **Managed DNS (Domain Name System)** service:

- **DNS is a collection of rules and records** which helps clients understand how to reach a server through URLs
- **Route 53 manages your domain's DNS records** - translates human-readable domain names to IP addresses

**In AWS, the most common records are**:

- **A record (IPv4)**: `www.google.com => 12.34.56.78` - maps domain to IPv4 address
- **AAAA record (IPv6)**: `www.google.com => 2001:0db8:85a3:0000:0000:8a2e:0370:7334` - maps domain to IPv6 address
- **CNAME**: `search.google.com => www.google.com` - hostname to hostname mapping
- **Alias**: `example.com => AWS resource` - maps to AWS resources (e.g., ELB, CloudFront, S3, RDS, etc.)
    - Alias records are AWS-specific and provide better integration with AWS services

> Route 53 is named after port 53, which is the port DNS uses. It's AWS's managed DNS service - instead of managing your own DNS servers, you use Route 53 to manage your domain's DNS records. DNS is like the phone book of the internet - when you type "www.amazon.com" in your browser, DNS translates that human-readable name into an IP address (like 54.239.28.85) that computers understand. Route 53 provides several advantages: it's highly available (automatically distributed across multiple locations), it integrates seamlessly with other AWS services (you can create Alias records that point directly to AWS resources like load balancers or S3 buckets), and it supports advanced routing policies (like routing users to the closest region based on latency, or routing to different servers based on health checks). Route 53 is a global service - it works the same way regardless of which AWS region you're in, and it can route traffic globally based on various policies.

### Route 53 - Diagram for A Record

![Route 53 - Diagram for A Record](assets/139-route-53-diagram.png)

### Route 53 Routing Policies

**Route 53 supports multiple routing policies** to control how traffic is distributed:

- **Simple Routing**: Basic routing - one record with one IP address
- **Weighted Routing**: Distribute traffic across multiple resources based on weights (e.g., 80% to server A, 20% to server B)
- **Latency-Based Routing**: Route users to the region with the lowest latency
- **Failover Routing**: Active-passive setup - route to primary, failover to secondary if primary is unhealthy
- **Geolocation Routing**: Route based on the geographic location of users
- **Geoproximity Routing**: Route based on geographic location with bias adjustments
- **Multivalue Answer Routing**: Return multiple healthy IP addresses (up to 8)

> **Need to know them at a high-level for the Cloud Practitioner** - understand the basic concepts and use cases

![Route 53 Routing Simple and Weighted Policies](assets/139-routing-simple-weight.png)

![Route 53 Routing Latency and Failover Policies](assets/139-routing-latency-failover.png)

> Routing policies determine how Route 53 responds to DNS queries. Simple routing is the most basic - one domain name points to one IP address. Weighted routing lets you distribute traffic - useful for A/B testing or gradually rolling out new versions (send 10% of traffic to the new version, 90% to the old version). Latency-based routing is powerful for global applications - Route 53 measures the latency from the user's location to each of your regions and routes them to the fastest one. Failover routing provides disaster recovery - you configure a primary and secondary endpoint, and Route 53 automatically routes to the secondary if the primary fails health checks. These policies can be combined - for example, you might use latency-based routing to send users to the closest region, and within that region, use weighted routing to distribute load across multiple servers. Understanding these policies is crucial for building resilient, high-performance global applications.

## 140. Route 53 Hands On
***This is a lab tutorial lesson***

## 141. CloudFront Overview

### AWS CloudFront

**AWS CloudFront** is a **Content Delivery Network (CDN)**:

- **Improves read performance** - content is cached at the edge locations
- **Improves user experience** - faster page loads and media streaming
- **Hundreds of Points of Presence globally** (edge locations, caches) - content stored close to users
- **DDoS protection** (because worldwide), integration with **AWS Shield**, **AWS Web Application Firewall (WAF)**

> CloudFront is AWS's global content delivery network. Think of it like having copies of your website stored in hundreds of locations around the world. When a user in Tokyo requests your website, instead of fetching it from your server in Virginia (which would take 200+ milliseconds), CloudFront serves it from a cache in Tokyo (which takes 10-20 milliseconds). This dramatically improves performance, especially for static content like images, videos, CSS files, and JavaScript. CloudFront works by caching content at "edge locations" - data centers located in major cities worldwide. When content is first requested, CloudFront fetches it from your origin server (like an S3 bucket or EC2 instance), caches it at the edge location, and serves it to users. Subsequent requests for the same content are served from the cache, which is much faster. CloudFront also provides built-in DDoS protection through AWS Shield, and you can integrate AWS WAF to filter malicious requests. This makes CloudFront not just a performance tool, but also a security tool. CloudFront is essential for any application that serves content to users globally - websites, mobile apps, video streaming, software downloads, etc.

![CloudFront Map](assets/141-cloudfront-map.png)

### CloudFront - Origins

**CloudFront Origins** are the sources where CloudFront fetches content from. CloudFront supports several origin types:

- **S3 Bucket**
    - **For distributed files and caching them at the edge** - static content like images, videos, documents
    - **For uploading files to S3 through CloudFront** - can handle both downloads and uploads
    - **Secured using Origin Access Control (OAC)** - prevents direct S3 access, forces CloudFront usage

- **VPC Origin**
    - **For applications hosted in VPC private subnets** - applications not publicly accessible
    - **Application Load Balancer / Network Load Balancer / EC2 Instances** - various backend options
    - Requires VPC integration and security configuration

- **Custom Origin (HTTP)**
    - **S3 website** (must first enable the bucket as a static S3 website)
    - **Any public HTTP backend you want** - your own web servers, APIs, etc.

> Origins are where your content lives - CloudFront is just the delivery mechanism. S3 is the most common origin for static content - you store files in S3, and CloudFront caches and serves them globally. Origin Access Control (OAC) is important for security - it ensures that users can only access S3 content through CloudFront, not directly. This prevents users from bypassing CloudFront (and your CDN benefits) and also allows you to keep S3 buckets private. VPC origins are for dynamic content - if you have a web application running on EC2 instances in private subnets, you can use CloudFront to cache static parts while forwarding dynamic requests to your application. Custom origins give you flexibility - you can use any HTTP server as an origin, whether it's in AWS or elsewhere. The key is that CloudFront sits in front of your origin, caching content and reducing load on your origin servers.

### CloudFront at a high level

![CloudFront at a High Level](assets/141-cloudfront-high-level.png)

### CloudFront - S3 as an Origin

**S3 is the most common CloudFront origin** for static content delivery:

![CloudFront - S3 as an Origin](assets/141-cloudfront-s3-as-an-origin.png)

### CloudFront vs S3 Cross-Region Replication

Understanding when to use **CloudFront** versus **S3 Cross-Region Replication**:

**CloudFront**:
    - **Global Edge network** - hundreds of edge locations worldwide
    - **Files are cached for a TTL** (maybe a day) - content is cached, not permanently stored
    - **Great for static content that must be available everywhere** - images, videos, CSS, JavaScript
    - **Content is served from cache** - reduces origin load

**S3 Cross-Region Replication**:
    - **Must be set up for each region** you want replication to happen - explicit region selection
    - **Files are updated in near real-time** - actual copies stored in multiple regions
    - **Read only** - replication is one-way
    - **Great for dynamic content** that needs to be available at low-latency in few regions
    - **Actual data storage** - not caching, but real replication

> These are two different approaches to global content delivery. CloudFront is about caching - it stores copies of your content temporarily at edge locations, and when the cache expires (TTL - Time To Live), it fetches fresh content from the origin. This is perfect for content that doesn't change often (like product images, videos, or software downloads) and needs to be fast everywhere. S3 Cross-Region Replication is about actual data replication - you're creating real copies of your data in multiple regions. This is more expensive (you're paying for storage in multiple regions) but ensures data is immediately available in those regions. Use CloudFront when you want global caching of static content. Use S3 Cross-Region Replication when you need actual data copies in specific regions (for compliance, disaster recovery, or low-latency access to frequently changing data). They can also be used together - replicate data to multiple regions, then use CloudFront to cache and serve it from those regions.

## 142. CloudFront Hands On
***This is a lab tutorial lesson***

## 143. S3 Transfer Acceleration

### S3 Transfer Acceleration

**S3 Transfer Acceleration** increases transfer speed by transferring files to an **AWS edge location**, which then forwards the data to the S3 bucket in the target region:

![S3 Transfer Acceleration](assets/143-s3-transfer-acceleration.png)

> S3 Transfer Acceleration is like using express shipping instead of regular mail. Normally, when you upload a file to S3, your data travels directly from your location to the S3 bucket's region over the public internet. If you're in Tokyo uploading to a bucket in Virginia, your data might take a slow, indirect route. S3 Transfer Acceleration uses CloudFront's edge network - you upload to the nearest edge location (which might be in Tokyo), and then AWS uses its optimized internal network to transfer the data to your S3 bucket in Virginia. AWS's internal network is much faster and more reliable than the public internet, so even though your data travels further (Tokyo → Edge Location → Virginia), it arrives faster. This is especially beneficial when uploading large files or when you're far from your S3 bucket's region. The acceleration is transparent - you just use a special endpoint (like `bucketname.s3-accelerate.amazonaws.com` instead of `bucketname.s3.amazonaws.com`), and AWS handles the rest. There's a small additional cost for the acceleration service, but for large file transfers or when speed is critical, it's often worth it.

***This is a lab tutorial lesson***

## 144. AWS Global Accelerator

### AWS Global Accelerator

**AWS Global Accelerator** improves global application availability and performance using the AWS global network:

- **Leverage the AWS internal network** to optimize the route to your application (60% improvement)
- **2 Anycast IP addresses are created** for your application and traffic is sent through Edge Locations
- **Provides static IP addresses** that don't change - simplifies firewall rules
- **Automatic failover** between regions if one becomes unavailable

![AWS Global Accelerator](assets/144-aws-global-accelerator.png)

![AWS Global Accelerator Compare](assets/144-aws-ga-compare.png)

> Global Accelerator is like having a smart traffic director for your application. Instead of users connecting directly to your application's IP address (which might be in a specific region), they connect to Global Accelerator's static IP addresses. Global Accelerator then routes their traffic over AWS's optimized internal network to the best endpoint (based on health, geography, and routing policies). The "Anycast IP" concept means the same IP address exists at multiple edge locations - when a user connects, they're automatically routed to the nearest edge location, which then forwards traffic to your application over AWS's fast internal network. This provides several benefits: (1) Faster performance - AWS's internal network is faster than the public internet, (2) Static IPs - your application gets fixed IP addresses that don't change, making firewall configuration easier, (3) Automatic failover - if one region fails, traffic automatically routes to healthy regions, (4) Health-based routing - traffic is automatically routed away from unhealthy endpoints. Global Accelerator is particularly useful for applications that need consistent performance, static IP addresses, or fast regional failover.

### AWS Global Accelerator vs CloudFront

**They both use the AWS global network and its edge locations** around the world, and **both services integrate with AWS Shield** for DDoS protection, but they serve different purposes:

**CloudFront - Content Delivery Network (CDN)**:
    - **Improves performance for your cacheable content** (such as images and videos)
    - **Content is served at the edge** - cached content delivered from edge locations
    - **Best for**: Static content, websites, media streaming
    - **Caching**: Yes - content is cached at edge locations

**Global Accelerator**:
    - **No caching** - proxying packets at the edge to applications running in one or more AWS Regions
    - **Improves performance for a wide range of applications** over TCP or UDP
    - **Good for HTTP use cases that require static IP addresses** - fixed IPs that don't change
    - **Good for HTTP use cases that require deterministic, fast regional failover** - automatic failover
    - **Best for**: Dynamic applications, APIs, non-HTTP traffic (TCP/UDP)
    - **Caching**: No - traffic is proxied, not cached

> The key difference is caching. CloudFront caches content at edge locations - if 1000 users request the same image, CloudFront serves it from cache 999 times (after the first request fetches it from origin). Global Accelerator doesn't cache - it's a proxy that routes every request to your application, but it routes over AWS's fast internal network. Use CloudFront when you have cacheable content (static websites, images, videos, software downloads) that benefits from being served from edge locations. Use Global Accelerator when you have dynamic applications (APIs, web applications, gaming servers) that can't be cached but need fast, reliable routing and failover. They can also be used together - use CloudFront to cache static content and Global Accelerator to route dynamic API requests to your backend.

## 145. AWS Outposts

### AWS Outposts

**AWS Outposts** brings AWS infrastructure and services to your on-premises data center:

- **Hybrid Cloud**: Businesses that keep an on-premises infrastructure alongside a cloud infrastructure
- **Therefore, two ways of dealing with IT systems**:
    - **One for the AWS cloud** (using the AWS console, CLI, and AWS APIs)
    - **One for their on-premises infrastructure** (traditional IT management)
- **AWS Outposts are "server racks"** that offer the same AWS infrastructure, services, APIs & tools to build your own applications on-premises just as in the cloud
- **AWS will set up and manage "Outposts Racks"** within your on-premises infrastructure and you can start leveraging AWS services on-premises
- **You are responsible for the Outposts Rack physical security** - AWS manages the infrastructure, you secure the facility

> AWS Outposts is like having a piece of AWS in your own data center. Many organizations want to use AWS services but have requirements that keep some infrastructure on-premises - maybe for data residency (laws requiring data to stay in a specific country), low-latency requirements (applications that need sub-millisecond latency to on-premises systems), or compliance reasons. Outposts solves this by installing AWS-managed server racks in your data center. These racks run the same AWS services (EC2, EBS, ECS, RDS, etc.) that you use in the cloud, but they're physically in your facility. You manage them through the same AWS console, CLI, and APIs - it's a seamless experience. AWS handles the hardware, software updates, and infrastructure management, while you're responsible for physical security (who can access the data center) and power/cooling. This creates a true hybrid cloud - you can run some workloads in AWS regions and some on Outposts, all managed through the same interface. Outposts is particularly valuable for organizations migrating to the cloud gradually, or for applications that need to stay on-premises but benefit from AWS's managed services and APIs.

![AWS Outposts](assets/145-aws-outposts.png)

**Benefits**:
    - **Low-latency access to on-premises systems** - applications can access on-premises databases and systems with minimal latency
    - **Local data processing** - process data locally without sending it to the cloud
    - **Data residency** - keep data in specific geographic locations for compliance
    - **Easier migration from on-premises to the cloud** - use the same APIs and tools
    - **Fully managed service** - AWS handles infrastructure management

**Some services that work on Outposts**:

![Services Work on Outposts](assets/145-services-work-on-outposts.png)

## 146. AWS Wavelength

### AWS Wavelength

**AWS Wavelength** brings AWS services to the edge of 5G networks:

- **Wavelength Zones are infrastructure deployments** embedded within the telecommunications providers' datacenters at the edge of the 5G networks
- **Brings AWS services to the edge of the 5G networks** - EC2, EBS, VPC, etc.
- **Ultra-low latency applications** through 5G networks - single-digit millisecond latency
- **Traffic doesn't leave the Communication Service Provider's (CSP) network** - stays on carrier network
- **High-bandwidth and secure connection** to the parent AWS Region
- **No additional charges or service agreements** with carriers - pay only AWS usage
- **Use cases**: Smart Cities, ML-assisted diagnostics, Connected Vehicles, Interactive Live Video Streams, AR/VR Real-time Gaming...

> AWS Wavelength is like having AWS infrastructure inside 5G cell towers. Traditional cloud computing has latency - even with the fastest connections, there's delay as data travels from a device, through the carrier's network, to the internet, to AWS, and back. For applications that need ultra-low latency (like autonomous vehicles making split-second decisions, or AR/VR applications that need instant response), this delay is unacceptable. Wavelength solves this by deploying AWS infrastructure (EC2, EBS, VPC) directly in the carrier's data centers, at the edge of the 5G network. When a 5G device connects, instead of traffic going: Device → 5G Network → Internet → AWS Region, it goes: Device → 5G Network → Wavelength Zone (AWS infrastructure in the carrier's data center). This eliminates the internet hop, reducing latency from 50-100 milliseconds to 5-10 milliseconds. The Wavelength Zone is still connected to a parent AWS Region, so you can use other AWS services, but the compute happens at the edge. This is perfect for applications that need real-time processing - autonomous vehicles processing sensor data, AR/VR applications rendering in real-time, or smart city applications that need instant responses.

![AWS WaveLength](assets/146-aws-wavelength.png)

## 147. AWS Local Zones

**AWS Local Zones** bring AWS resources (compute, database, storage, etc.) closer to your users:

- **Place AWS resources in specific metropolitan areas** - closer than regions but not as close as edge locations
- **Good for latency-sensitive applications** - reduce latency for users in specific cities
- **Extend VPC from parent region** - Local Zones are extensions of a parent AWS region
- **Use cases**: Real-time gaming, media content creation, machine learning inference, financial trading

> AWS Local Zones are like mini-regions in major metropolitan areas. While AWS Regions are large geographic areas (like "US East" covering multiple states), Local Zones are in specific cities (like Los Angeles or Boston). They provide AWS compute, storage, and database services closer to end users, reducing latency for applications that need it. Unlike Wavelength (which is embedded in 5G carrier networks), Local Zones are AWS infrastructure in AWS data centers, just located in cities rather than in the larger regional data centers. Local Zones extend your VPC from the parent region, so you can seamlessly use resources in both the region and the Local Zone. This is perfect for applications that serve users in specific metropolitan areas and need lower latency than a full region can provide, but don't need the extreme low latency of Wavelength. For example, a gaming company might deploy game servers in a Local Zone near Los Angeles to serve West Coast players with lower latency.

***This is a lab tutorial lesson***

## 148. Global Applications Architecture

Understanding different architecture patterns for global applications:

**Single Region Architectures**:
- **Single AZ**: All resources in one Availability Zone - simple but not highly available
- **Multi-AZ**: Resources distributed across multiple Availability Zones - high availability within a region

**Multi-Region Architectures**:
- **Passive**: Secondary region is ready but not serving traffic - used for disaster recovery
- **Active**: Both regions serve traffic - active-active setup for global load distribution

> Architecture decisions depend on your availability and performance requirements. Single region, single AZ is the simplest but provides no redundancy - if that AZ fails, your application is down. Multi-AZ within a region provides high availability - if one AZ fails, resources in other AZs continue operating. Multi-region architectures provide disaster recovery and global performance. Passive multi-region means you have a complete copy of your application in another region, but it's only used if the primary region fails (disaster recovery). Active multi-region means both regions serve traffic simultaneously - users are routed to the closest or best-performing region. This provides both disaster recovery and performance benefits, but is more complex and expensive. The choice depends on your RTO (Recovery Time Objective) and RPO (Recovery Point Objective) requirements, as well as your user distribution and performance needs.

![Single Region with Single and Multi AZ](assets/148-single-region-single-az-vs-multi-az.png)

![Multi Region with Passive and Active](assets/148-multi-region-passive-vs-active.png)

## 149. Leveraging the AWS Global Infrastructure Summary

### Global Applications in AWS - Summary

**Global DNS: Route 53**
    - **Great to route users to the closest deployment** with least latency
    - **Great for disaster recovery strategies** - automatic failover between regions
    - Multiple routing policies (latency-based, failover, weighted, etc.)

**Global Content Delivery Network (CDN): CloudFront**
    - **Replicate part of your application to AWS Edge Locations** - decrease latency
    - **Cache common requests** - improved user experience and decreased latency
    - Hundreds of edge locations worldwide

**S3 Transfer Acceleration**
    - **Accelerate global uploads & downloads** into Amazon S3
    - Uses CloudFront edge network for optimized transfers

**AWS Global Accelerator**
    - **Improve global application availability and performance** using the AWS global network
    - Provides static IP addresses and intelligent routing
    - Automatic failover between regions

**AWS Outposts**
    - **Deploy Outposts Racks in your own Data Centers** to extend AWS services
    - Hybrid cloud - AWS services on-premises
    - Same APIs and management as AWS cloud

**AWS Wavelength**
    - **Brings AWS services to the edge of the 5G networks**
    - **Ultra-low latency applications** - single-digit millisecond latency
    - Embedded in carrier data centers

**AWS Local Zones**
    - **Bring AWS resources** (compute, database, storage, etc.) **closer to your users**
    - **Good for latency-sensitive applications** - metropolitan area deployments
    - Extend VPC from parent region
