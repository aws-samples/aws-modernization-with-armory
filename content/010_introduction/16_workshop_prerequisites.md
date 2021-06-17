---
title: "Workshop Prerequisites"
chapter: true
weight: 16
---

# Workshop Prerequisites

There are a few prerequisite tasks you must perform before getting started on this workshop. These are:

1. Access to an AWS account with proper permissions. See AWS Account Setup below
   
1. Armory Enterprise provisioned via AWS QuickStart


## Setting up your AWS account

{{% notice warning %}}
You are responsible for the cost of the AWS services used while running this workshop in your AWS account. We highly recommend you to go to the [request AWS credit page](/030_self_guided_setup/30_request_credit.html) so you can run this workshop without any charge to you.
{{% /notice %}}

1. If you don't already have an AWS account with Administrator access:
[create one now by clicking here](https://aws.amazon.com/getting-started/)

1. Once you have an AWS account, ensure you are following the remaining workshop steps
as an IAM user with administrator access to the AWS account:
[Create a new IAM user to use for the workshop](https://console.aws.amazon.com/iam/home?#/users$new)
   {{%expand "Enter the user details"%}}![Create User](/images/iam-1-create-user.png){{% /expand%}}
   {{%expand "Attach the AdministratorAccess IAM Policy"%}}![Attach Policy](/images/iam-2-attach-policy.png){{% /expand%}}
   {{%expand "Create the new user"%}}![Finish Creation](/images/iam-3-create-user.png){{% /expand%}}
   {{%expand "Take note of the login URL and save for the use within workshop"%}}![Login url](/images/iam-4-save-url.png){{% /expand%}}

1. Generate an SSH Key pair for the targeted AWS region. You can navigate to [EC2 Home](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Home:) and find the "Key Pairs" link in the left-hand navigation under "Network & Security". Create one if you do not have any. You will need it as the parameter for Armory QuickStart (for Bastion host access)
![Create SSH Pair](/images/ec2-ssh-keypair.png)