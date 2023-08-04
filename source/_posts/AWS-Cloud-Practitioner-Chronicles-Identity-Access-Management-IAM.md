---
title: AWS Cloud Practitioner Chronicles - Identity Access Management (IAM)
date: 2023-05-07 21:55:00 +0800
tags: [aws, cloud computing, aws cloud practitioner]
---

![AWS](https://d1.awsstatic.com/howitworks_IAM_110321.8b2290727bb2022d54416e099c87ad9dc64be5d5.jpg "AWS")

For my second week of preparation for the AWS Cloud Practitioner certification, I will be exploring the topic "Identity and Access Management(IAM)" in AWS. IAM is one of the most crucial aspects of cloud computing which enables organizations to manage access to AWS services and resources securely. 

In this blog post, I will discuss the basics of IAM in AWS, including user and group management, policies, and authentication mechanisms.

## An Overview

IAM is a core AWS service that we use to authenticate and get authorised to access various resources. With IAM, we can create and manage user accounts, groups, and roles, and define policies that grant or deny access. Depending on our use cases and requirements, we can use one of these choices to access IAM:

* AWS CLI
* AWS Management Console
* AWS IAM API
* AWS SDKs

## IAM Entities

![AWS](https://digitalcloud.training/wp-content/uploads/2022/02/iam-users-groups-roles-policies.png "AWS")

### IAM Users

IAM users are entities that we create in AWS to represent people or services that need to interact with our AWS resources. Here are some of the essentials of them:

* Users have no permissions by default.
* AWS allows us to create up to 500 IAM users per account. Each user has a friendly name something like **Semih** and has an Amazon Resource Name(ARN) which is something like **arn:aws:iam:436494181:user/Semih**.
* Root user has full permissions but it's generally best practice to avoid using the root user and enable **MFA**.

### Federated Users
These kind of users are users who are authenticated and authorized by another source. For instance, we might have an account with Google or Microsoft or Facebook and we can log in there and gain access to resources. When a federated user tries to access an AWS resource, the AWS security token service (STS) verifies the user's identity and retrieves temporary security credentials that are associated with an IAM role.

### Groups
A group is basically a collection of IAM users that we can organize together in order to apply permissions to them by using policies. Organizing users into various groups may be quite efficent and help us to use AWS resources more effectively. To give an example, we might create a group called "Developers" and add multiple users to it who need access to AWS resources for development purposes. And then when we apply the related policy into this group all users in the "Developers" group will inherit the permissions defined in the policy.

### Roles
Roles are also one of the identities and with them we can easily delegate specific permissions that can be assumed by users, apps, and services without the need to share credentials like password or access keys. What's more, a role can also be assigned to a federated user and they are given a temporary set of security credentials that allows them to access the AWS resources specified in the role's policies.

### Policies

![AWS](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2018/01/30/AR2_0118_a.png "AWS")
Policies in AWS IAM, are documents that define permissions and are written in JSON format as shown in the image above. They allow us to specify which AWS resources users and groups can access and what actions they can perform on those resources. Note that all permissions are implicitly denied by default. Therefore, we need to attach policies to IAM users, groups, and roles to grant them the necessary permissions to access resources.



In conclusion, I gave an overview of IAM in AWS, discussing the different IAM entities such as users, groups, roles, and policies. I also highlighted the importance of IAM in managing access to AWS resources securely. I hope to dive into AWS Compute Services next week!