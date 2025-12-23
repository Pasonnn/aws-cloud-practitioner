# Section 11: Deployments & Managing Infrastructure at Scale

## 123. CloudFormation Overview

### What is CloudFormation

- CloudFormation is a declarative way of outlining your AWS Infrastructure, for any resources (most of them are supported).
- For example, within a CloudFormation template, you say:
    - I want a security group
    - I want two EC2 instances using this security group
    - I want an S3 bucket
    - I want a load balancer (ELB) in front of these machines
- Then CloudFormation creates those for you, in the right order, with the exact configuration that you specify

### Benefits of AWS CloudFormation

- Infrastructure as code
    - No resources are manually created, which is excellent for control
    - Changes to the infrastructure are reviewed through code
- Cost
    - Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
    - You can estimate the costs of your resources using the CloudFormation template
    - Savings strategy: In Dev, you could automation deletion of templates at 5 PM and recreated at 8 AM, safely

- Productivity
    - Ability to destroy and re-create an infrastructure on the cloud on the fly
    - Automated generation of Diagram for your templates
    - Declarative programming (no need to figure out ordering and orchestration)

- Don't re-invent the wheel
    - Leverage existing templates on the web
    - Leverate the documentation

- Supports (almost) all AWS resources:
    - Everything we'll see in this course is supported
    - You can use "custom resources" for resources that are not supported

### CloudFormation + Infrastructure Composer
- Example: WordPress CloudFormation Stack
- We can see all the resouces
- We can see the relations between the components

![CloudFormation + Infrastructure Composer](assets/123-cloudformation-infra-composer.png)

## 124. CloudFormation Hands On

## 125. CDK Overview

## 126. Beanstalk Overview

## 127. Beanstalk Hands On

## 128. CodeDeploy Overview

## 129. IMPORTANT: CodeCommit Discontinuation

## 130. CodeCommit Overview

## 131. CodeBuild Overview

## 132. CodePipeline Overview

## 133. CodeArtifact Overview

## 134. Systems Manager (SSM) Overview

## 135. SSM Session Manager

## 136. SSM Parameter Store

## 137. Deployment Summary
