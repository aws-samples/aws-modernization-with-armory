---
title: "1. Armory AWS QuickStart"
chapter: true
weight: 10
---
## Armory AWS Quickstart
https://aws.amazon.com/quickstart/architecture/armory-enterprise/

Armory provides a scalable and flexible platform for automating software delivery. To help companies deploy software into multiple clouds, the core of Armory’s platform is powered by Operator, an open-source, continuous-delivery platform developed by Netflix and Google. Continuous delivery is a process that builds production software on a consistent basis.

Armory Operator acts as a workflow engine by combining build, provision, and deploy steps into an automated pipeline. It deploys your workloads (for example, containers, packages, and Amazon Machine Images) to your AWS environment, including Amazon Elastic Compute Cloud (Amazon EC2), Amazon Elastic Kubernetes Service (Amazon EKS), Amazon Elastic Container Service (Amazon ECS), and AWS Lambda.

With Armory's integrations, you can automate your code from commit to production, where users can then monitor applications, scale up, scale down, roll back, or roll forward. You can use Armory to view and automate all of these actions.

Use this Quick Start to set up the following Armory environment on AWS:

A highly available architecture that spans three Availability Zones.
A virtual private cloud (VPC) configured with public and private subnets, according to AWS best practices, to provide you with your own virtual network on AWS.
In the public subnets:
* A Linux bastion host, configured for Kubernetes, in an Auto Scaling group to allow inbound Secure Shell (SSH) access to Amazon Elastic Compute Cloud (Amazon EC2) instances in the private subnets.
* A managed network address translation (NAT) gateway to allow outbound internet access for resources in the private subnets.
In the private subnets:
* A group of Kubernetes nodes.
* ElastiCache Redis for caching storage for Orca and Clouddriver.
* Amazon Aurora for persistent storage of Orca and Clouddriver assets.
* Amazon EKS for the underlying Kubernetes infrastructure and platform.
* Amazon Simple Storage Service (Amazon S3) for persistent storage of Armory objects.
* An Armory Operator installation in an Amazon EKS cluster, which creates the Kubernetes control plane.
