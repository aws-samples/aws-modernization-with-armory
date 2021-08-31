---
title: "Setting up Armory Quickstart"
chapter: false
draft: false
weight: 13
---

With Armory's integrations, you can automate your code from commit to production, where users can then monitor applications, scale up, scale down, roll back, or roll forward. You can use Armory to view and automate all of these actions.

Use Armory's [Quick Start](https://aws.amazon.com/quickstart/architecture/armory-enterprise/) to set up the following Armory environment on AWS:

* A highly available architecture that spans three Availability Zones

* A virtual private cloud (VPC) configured with public and private subnets, according to AWS best practices, to provide you with your own virtual network on AWS

* In the public subnets:
  * A Linux bastion host, configured for Kubernetes, in an Auto Scaling group to allow inbound Secure Shell (SSH) access to Amazon Elastic Compute Cloud (Amazon EC2) instances in the private subnets
  * A managed network address translation (NAT) gateway to allow outbound internet access for resources in the private subnets

* In the private subnets:
  * A group of Kubernetes nodes
  * ElastiCache Redis for caching storage for Orca and Clouddriver
  * Amazon Aurora for persistent storage of Orca and Clouddriver assets
  * Amazon EKS for the underlying Kubernetes infrastructure and platform
  * Amazon Simple Storage Service (Amazon S3) for persistent storage of Armory objects
  * An Armory Operator installation in an Amazon EKS cluster, which creates the Kubernetes control plane.

![Armory QuickStart](/images/armory-enterprise-architecture-diagram.png)

## Installation

1. Log into your AWS Account
   
1. Navigate to the CloudFormation landing page for the [Armory Enterprise AWS Quickstart](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Faws-quickstart.s3.us-east-1.amazonaws.com%2Fquickstart-armory-enterprise%2Ftemplates%2Fspinnaker-entrypoint-new-vpc.template.yml&stackName=Armory-Spinnaker-on-EKS-New-VPC) as shown below
![CF Landing Page](/images/armory-cf-landing-page.png)

1. Confirm the AWS Region you are working is your intended region
   
1. Click **Next** to proceed

