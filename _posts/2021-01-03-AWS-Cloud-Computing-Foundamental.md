---
layout:     post
title:      AWS Cloud Computing Foundamental
subtitle:   AWS Identity and Access Management(IAM), Elastic Compute Cloud(EC2)
date:       2021-01-23
author:     Shuo Wang
header-img: img/post-bg-aws.png
catalog: true
tags:
    - AWS
    - Cloud Computing
    - IAM
    - EC2
---


# Day1 What is AWS Identity and Access Management(IAM)

--

**AWS Identity and Access Management(IAM)** is a web service that enables Amazon Web Services(AWS) customers to manage users and user permissions in AWS. With IAM, you can centrally manage **users, security, credentials** such as access keys and **permissions** that control which AWS resources users can access.

**Manage IAM Users and their access:**
You can create Users and assign them individual security credentials (access keys, passwords, and multi-factor authentication devices). You can manage permissions to control which operations a User can perform.

**Manage IAM Roles and their permissions:**
An IAM Role is similar to a User, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a Role is intended to be assumable by anyone who needs it.

**Manage federated users and their permissions:**
You can enable identity federation to allow existing users in your enterprise to access the AWS Management Console, to call AWS APIs and to access resources, without the need to create an IAM User for each identity.

---

## My learned

Availability Zones (AZs): physical data center;
Regions: server location in different cities; (one region has many AZs)
Edge Locations: for higher density users, which loads the high frequency stuff into memory to make a lower latency, fast response and decrease system burden.
Regional Edge Caches: for lower access things but in different regions, which provides a higher and faster access.

one AZ has many Data Center
one Region has many AZ(Availability Zone) (at least 2)
each AZ is isolated with each other but closer with each other combined with lower latency.

AWS AMI:
Users:
group: many users have same permissions

Roles: **the service in AWS** communicate with other services in AWS e.g. EC to S3
policies: the permission of document for the templates for specific access rights; How many resources can be accessed.
one Role has many policies.

# Day2 What is Elastic Cloud Computing(EC2)?
