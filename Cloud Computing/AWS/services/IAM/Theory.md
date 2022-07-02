# Introduction
AWS Identity and Access Management (IAM) provides fine-grained access control across all of AWS. With IAM, one can specify who can access which services and resources, and under which conditions. With IAM policies, one manages permissions to the workforce and systems to ensure least-privilege permissions. It is an AWS service that is offered at no additional charge.

**Service Scope:** Global

# Concepts
## Users & Groups
* Users are the people in an organisation that can be grouped
* Groups can contain only people and not other groups
* Users can belong to 0 (bad practice) or multiple groups
* Root user gets created by default but should avoid using unless absolutely necessary

## Permissions
* Permissions of the users and groups are managed using JSON documents called *policies*
* In AWS, least priviledge principle is used when providing permissions, it means that the user should not have more permissions than required
* There are 2 types of policies: Inline (individual to the user) and Group

    ### Structure of a policy
    * _Version:_ policy language version
    * _Id:_ an identifier for the policy (optional)
    * _Statement:_ one or more individual statements (required)
        * _Sid:_ an identifier for the statement (optional)
        * _Effect:_ whether the statement allows or denies access (Allow, Deny)
        * _Principal:_ account/user/role to which this policy applied to
        * _Action:_ list of actions this policy allows or denies
        * _Resource:_ list of resources to which the actions applied to
        * _Condition:_ conditions for when this policy is in effect (optional)
    
    Example:
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowServices",
                "Effect": "Allow",
                "Action": [
                    "s3:*",
                    "cloudwatch:*",
                    "ec2:*"
                ],
                "Resource": "*"
            },
            {
                "Sid": "AllowIAMConsoleForCredentials",
                "Effect": "Allow",
                "Action": [
                    "iam:ListUsers",
                    "iam:GetAccountPasswordPolicy"
                ],
                "Resource": "*"
            },
            {
                "Sid": "AllowManageOwnPasswordAndAccessKeys",
                "Effect": "Allow",
                "Action": [
                    "iam:*AccessKey*",
                    "iam:ChangePassword",
                    "iam:GetUser",
                    "iam:*LoginProfile*"
                ],
                "Resource": ["arn:aws:iam::*:user/${aws:username}"]
            },
            {
                "Sid": "DenyS3Logs",
                "Effect": "Deny",
                "Action": "s3:*",
                "Resource": [
                    "arn:aws:s3:::logs",
                    "arn:aws:s3:::logs/*"
                ]
            },
            {
                "Sid": "DenyEC2Production",
                "Effect": "Deny",
                "Action": "ec2:*",
                "Resource": "arn:aws:ec2:*:*:instance/i-1234567890abcdef0"
            }
        ]
    }
    ```

# Password Policy
* Strong passwords = higher security for your account
* In AWS, you can setup a password policy:
    * Set a minimum password length
    * Require specific character types:
        * including uppercase letters
        * lowercase letters
        * numbers
        * non-alphanumeric characters
    * Allow all IAM users to change their own passwords
    * Require users to change their password after some time (password expiration)
    * Prevent password re-use

# Multi-Factor Authentication (MFA)
* Users have access to your account and can possibly change configurations or delete resources in your AWS account
* **You want to protect your root accounts and IAM users**
* _MFA = password you know + security device you own_
* The benefit of MFA is that if the password is stolen or hacked, the account is not compromised
* Device options:
    * _Virtual MFA device:_ Support for multiple tokens on a single device. Example - Authy, Google Authenticator
    * _Security Key:_ Support for multiple root and IAM users using a single security key. Example -  YubiKey by Yubico
    * _Other hardware MFA device:_: Example - Hardware Key Fob MFA Device by Gemalto, Hardware Key Fob MFA Device for AWS GovCloud (US)

# Roles for Services
* Some AWS service will need to perform actions on the user's behalf
* To do so, permissions are needed to be assigned to AWS services with IAM Roles
* Common roles:
    * EC2 Instance Roles
    * Lambda Function Roles
    * Roles for CloudFormation

# Security Tools
* IAM Credentials Report (account-level)
    * a report that lists all your account's users and the status of their various credentials
* IAM Access Advisor (user-level)
    * Access advisor shows the service permissions granted to a user and when those services were last accessed.
    * You can use this information to revise your policies.

# Ways to access to AWS
* To access AWS, you have three options:
    * AWS Management Console (protected by password + MFA)
    * AWS Command Line Interface (CLI): protected by access keys
    * AWS Software Developer Kit (SDK) - for code: protected by access keys
* Access Keys are generated through the AWS Console
* Users manage their own access keys
* Access Keys are secret, just like a password. Don’t share them
* Access Key ID ~= username
* Secret Access Key ~= password

# Shared Responsibity for IAM
+--------------------------------------------+------------------------------------------------------------+
| AWS                                        | User                                                       |
+============================================+============================================================+
| * Infrastructure (global network security) | * Users, Groups, Roles, Policies management and monitoring |
| * Configuration and vulnerability analysis | * Enable MFA on all accounts                               |
| * Compliance validation                    | * Rotate all your keys often                               |
|                                            | * Use IAM tools to apply for appropriate permissions       |
|                                            | * Analyse access patterns & review permissions             |
+--------------------------------------------+------------------------------------------------------------+

# Best Practices
* Don’t use the root account except for AWS account setup
* One physical user = One AWS user
* Assign users to groups and assign permissions to groups
* Create a strong password policy
* Use and enforce the use of Multi Factor Authentication (MFA)
* Create and use Roles for giving permissions to AWS services
* Use Access Keys for Programmatic Access (CLI / SDK)
* Audit permissions of your account with the IAM Credentials Report
* Never share IAM users & Access Keys

# Summary
* Users: mapped to a physical user, has a password for AWS Console
* Groups: contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: for EC2 instances or AWS services
* Security: MFA + Password Policy
* AWS CLI: manage your AWS services using the command-line
* AWS SDK: manage your AWS services using a programming language
* Access Keys: access AWS using the CLI or SDK
* Audit: IAM Credential Reports & IAM Access Advisor