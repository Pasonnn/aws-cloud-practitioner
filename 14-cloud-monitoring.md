# Section 14: Cloud Monitoring

## 158. CloudWatch Metrics & CloudWatch Alarms Overview

### Amazon CloudWatch Metrics
- CloudWatch provides metrics for every services in AWS
- Metric is a variable to monitor (CPU Utilization, Network In, ...)
- Metrics have timestamps
- Can create CloudWatch dashboards of metrics

### Example: CloudWatch Billing metric (us-east-1)
![Example of CloudWatch Billing Metric](assets/158-cloudwatch-billing-metric.png)

### Important Metrics
- EC2 instances: CPU Utilization, Status Check, Network (not RAM)
    - Default metrics every 5 minutes
    - Option for Detailed Monitoring ($$$): metrics every 1 minute
- EBS volumes: Disk Read/Writes
- S3 buckets: Bucket Size Bytes, Number Of Objects, All Requests
- Billing: Total Estimated Charge (only in us-east-1)
- Service Limits: how much you have been using a service API
- Custom metrics: push your own metrics

### Amazon CloudWatch Alarms
- Alarms are used to trigger notifications for any metric
- Alarm actions
    - Auto Scaling: increase or decrease EC2 instances "desired" count
    - EC2 Actions: stop, terminate, reboot or recover an EC2 instance
    - SNS notifications: send a notification into an SNS topic
- Various options (sampling, %, max, min, etc)
- Can choose the period on which to evaluate an alarm
- Example: create a billing alarm on the CloudWatch Billing metric
- Alarm States: OK, INSUFFICIENT_DATA, ALARM

## 159. CloudWatch Metrics & CloudWatch Alarms Hands On
***This is a lab tutorial lesson***

## 160. CloudWatch Logs Overview

### Amazon CloudWatch Logs
- CloudWatch Logs can collect log from:
    - Elastic Beanstalk: collection of logs from application
    - ECS: collection from containers
    - AWS Lambda: collection from function logs
    - CloudTrail based on filter
    - CloudWatch log agents: on EC2 machines or on-premises servers
    - Route53: Log DNS queries
- Enables real-time monitoring of logs
- Adjustable CloudWatch Logs retention

### CloudWatch Logs for EC2
- By default, no logs from your EC2 instance will go to CloudWatch
- You need to run a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permissions are correct
- The CloudWatch log agent can be setup on-premises too

![CloudWatch Logs for EC2](assets/160-cloudwatch-logs-for-ec2.png)

## 161. CloudWatch Logs Hands On
***This is a lab tutorial lesson***

## 162. EventBridge Overview (formerly CloudWatch Events)

## 163. EventBridge Hands On

## 164. CloudTrail Overview

## 165. CloudTrail Hands On

## 166. X-Ray Overview

## 167. CodeGuru Overview

## 168. AWS Health Dashboard

## 169. AWS Health Dashboard - Hands On

## 170. Cloud Monitoring Summary
