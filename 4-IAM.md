# Section 4: IAM - Identity and Access Management
## 14. IAM Introduction: Users, Groups,Policies

### IAM: Users & Groups
- IAM = Identity and Access Management, Global service
- Root account created by default, should not be used or shared
- Users are people within your organization, and can be grouped
- Groups only contain users, not other groups

![IAM: Users and Groups](assets/14-iam-users-group.png)

### IAM: Permissions
- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the users
- In AWS you apply the least privilege principle: do not give more permissions than a user needs

![IAM: Permissions Json](assets/14-iam-permissions.png)

## 15. IAM Users & Groups Hands On
***This is a lab tutorial lesson***

## 16. AWS Console Simultaneous Sign-in
***This is a lab tutorial lesson***

## 17. IAM Policies

### IAM Policies inheritance
![IAM Policies inheritance](assets/17-iam-policies-inheritance.png)

### IAM Policies Structure
- Consists of
    - Version: policy language version, always include "2012-10-17"
    - Id: an identifier for the policy (optional)
    - Statement: one or more individual statements (required)
- Statements consists of
    - Sid: an identifier for the statement (optional)
    - Effect: whether the statement allows or denied access (Allow, Deny)
    - Principal: account/user/role to which this policy applied to
    - Action: list of actions this policy allows or denies
    - Resource: list of resources to which the actions applied to
    - Condition: conditions of resources to which the actions applied to
    - Condition: conditions for when this policy is in effect (optional)

![IAM Policies Structure](assets/17-iam-policies-structure.png)

## 18. IAM Policies Hands On
***This is a lab tutorial lesson***

## 19. IAM MFA Overview
### IAM - Password Policy
- Strong password = higher security for your account
- In AWS, youc an setup a password policy:
    - Set a minimum password length
    - Require specific character types:
        - including uppercase letters
        - lowercase letters
        - numbers
        - non-alphanumeric characters
    - Allow all IAM users to change their own passwords
    - Require users to change their password after some time (password expiration)
    - Prevent password re-use

### Multi Factor Authentication - MFA
- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- You want to protect your Root Accounts and IAM users
- MFA = password you know + security device you own
- Main benefit of MFA: <u>if a password is stolen or hacked, the account is not compromised</u>

### MFA devices options in AWS
- Virtual MFA device: support for multiple tokens on a single device
- Universal 2nd Factor (U2F) Security Key: Support for multiple root and IAM users using a single security key
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)

## 20. IAM MFA Hands On
***This is a lab tutorial lesson***

## 21. AWS Access Keys, CLI and SDK
### How can users access AWS?
- To access AWS, you have three options:
    - AWS Management Console (protected by password + MFA)
    - AWS Command Line Interface (CLI): protected by access keys
    - AWS Software Developer Kit (SDK) - for code: protected by access keys
- Access Keys are generated through the AWS Console
- Users manage their own access keys
- <u>Access Keys are secret, just like a password, Do not share them</u>
- Access Key ID ~= username
- Secret Access Key ~= password

### Example Access Keys
![Example Access Keys](assets/20-example-access-keys.png)
- Access Key ID
- Secret Access Key
- <u>Remember: do not share your access keys</u>

### What is the AWS CLI?
- A tool that enables you to interact with AWS services using commands in your command-line shell
- Direct access to the public APIs of AWS services
- You can develop scripts to manage your resources
- It is open-source ***https://github.com/aws/aws-cli***
- Alternative to using AWS Management Console
![AWS CLI](assets/20-aws-cli.png)

### What is the AWS SDK?
- AWS Software Development Kit (AWS SDK)
- Language-specific APIs (set of libraries)
- Enables you to access and manage AWS services programmatically
- Embedded within your application
- Supports
    - SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
    - Mobile SDKs (Android, iOS, ...)
    - IoT Device SDKs (Embedded C, Andruino, ...)
- Example: AWS CLI is built on AWS SDK for Python

## 22. AWS CLI Setup on Windows
***This is a lab tutorial lesson***

## 23. AWS CLI Setup on Mac
***This is a lab tutorial lesson***

## 24. AWS CLI Setup on Linux
***This is a lab tutorial lesson***

## 25. AWS CLI Hands On
***This is a lab tutorial lesson***

## 26. AWS CloudShell
***This is a lab tutorial lesson***

## 27. IAM Roles for AWS Services
- Some AWS service will need to perform actions on your behalf
- To do so, we will assign permissions to AWS services with IAM Roles
- Common roles:
    - EC2 Instance Roles
    - Lambda Function Roles
    - Roles for CloudFormation

![IAM Roles for Services](assets/27-iam-role-for-services.png)

## 28. IAM Roles Hands On
***This is a lab tutorial lesson***

## 29. IAM Security Tools
- IAM Credentials Report (account-level)
    - a report that lists all your account's users and the status of their various credentials
- IAM Access Advisor (user-level)
    - Access advisor shows the service permissions granted to a user and when those services were last accessed
    - You can use this information to revise your policies

## 30. IAM Security Tools Hands On
***This is a lab tutorial lesson***

## 31. IAM Best Practices
- Do not use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication (MFA)
- Create and use Roles for giving permissions to AWS services
- Use Access Keys for Programmatic Access (CLI/SDK)
- Audit permissions of your account using IAM Credentials Report & IAM Access Advisor
- <u>Never share IAM users and Access Keys</u>

## 32. Shared Responsibility Model for IAM

**AWS**
- Infrastructure (global network security)
- Configuration and vulnerability analysis
- Compliance validation

**You**
- Users, Groups, Roles, Policies management and monitoring
- Enable MFA on all accounts
- Rotate all your keys often
- Use IAM tools to apply appropriate permissions
- Analyze access patterns and review permissions

## 33. IAM Summary
- Users: mapped to a physical user, has a password for AWS Console
- Groups: contains users only
- Policies: JSON document that outlines permissions for users or groups
- Roles: for EC2 instances or AWS services
- Security: MFA + Password Policy
- AWS CLI: manage your AWS services using the command-line
- AWS SDK: manage your AWS services using a programming language
- Access Keys: access AWS using the CLI or SDK
- Audit: IAM Credential Reports & IAM Access Advisor
