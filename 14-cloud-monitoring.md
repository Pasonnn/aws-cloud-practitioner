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

## 160. CloudWatch Logs Overview

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
