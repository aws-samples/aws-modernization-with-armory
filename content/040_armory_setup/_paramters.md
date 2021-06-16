---
title: "Parameters"
chapter: true
draft: false
weight: 1
---

# Parameters

The CloudFormation template provides an opportunity to provide values that will be used to customize the resources required for Armoryy Enterprise. The important values to to enter are 

- Availability Zones
- SSH key name
- Allowed external access CIDR
- Number of Availability zones (Needs to match the number of zones listed above)
- EKS Public Access Point
- Instance type (Should be a t3.xlarge or greater)

After entering the desired values, press "Next"

![stack-details](/images/stack-details.png)