---
layout:     post
title:      AWS Cloud Computing Foundamental
subtitle:   AWS Identity and Access Management(IAM), Elastic Compute Cloud(EC2)
date:       2021-01-23
author:     Shuo Wang
header-img: img/post-bg-awslogo.jpg
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

Roles: **the service in AWS** communicate with other services in AWS e.g. EC2, S3

policies: the permission of document for the templates for specific access rights; How many resources can be accessed.

one Role has many policies.

# Day2 What is Elastic Cloud Computing(EC2)?

A virtualized and abstracted subset of a physical server. It'll have access to storage, memroy and a network surface.

After you configure your instance's operating system, the OS is defined by the Amazon Machine Image(AMI) you choose, and the hardware follows the instance type.

Amazon Quick Start AMIs: include various releases of Linux or Windows Server OSs and some specialty images for performing common operations.

AWS Marketplace AMIs: from the AWS Marketplace are official, production-ready images provided and supported by industry vendors like SAP and Cisco.

Community AMIs: these images are AMIs created and maintained by independent vendors and are usually built to meet a specific need. This is a good catalog to search if you're palnning an application built on a custom combination of software resources.

## Instance Types
Instance Type Family:

Accelerated computing: P3, P2, G3, F1 (machine learning, Neural network)

based on cost for the instance types:

**On-Demand Instances:** when you use, you cost; before have a higher volumn to use it. e.g. Black Friday. (按需)

**Reserved Instances:** a contract that server one year(maybe). it becomes cheaper with longer development. (预留)

**Spot Instances:** during peak computing level, it needs more money. (竞价)

**Scheduled Reserved Instances:** periodically use server. (计划的预留)

**Dedicated Instances & Dedicated Hosts:** VIP~!(专用) 

## What Is Virtual Private Clouds (VPCs)?
VPCs are easy-to-use AWS network organizers and great tools for organizing your infrastructure, which can be easy to isolate the instances in one VPC from whatever else you have running. eg. one VPC for application development, another for beta testing and a third for production.

EC2 is located in the VPCs.

