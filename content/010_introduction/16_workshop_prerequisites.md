---
title: "Workshop Prerequisites"
chapter: true
weight: 16
---

# Workshop Prerequisites

There are a few prerequisite tasks you must perform before getting started on this workshop. These are:

1. Access to an AWS account with proper permissions. See AWS Account Setup below.
1. Armory Enterprise provisioned via AWS QuickStart


## Setting up your AWS account

{{% children %}}

{{% notice warning %}}
You are responsible for the cost of the AWS services used while running this workshop in your AWS account. We highly recommend you to go to the [request AWS credit page](/030_self_guided_setup/30_request_credit.html) so you can run this workshop without any charge to you.
{{% /notice %}}

1. If you don't already have an AWS account with Administrator access: 
[create one now by clicking here](https://aws.amazon.com/getting-started/)

1. Once you have an AWS account, ensure you are following the remaining workshop steps
as an IAM user with administrator access to the AWS account:
[Create a new IAM user to use for the workshop](https://console.aws.amazon.com/iam/home?#/users$new)

1. Enter the user details:
[create user](/images/20_prerequisites/iam-1-create-user.png)

1. Attach the AdministratorAccess IAM Policy:
[attach policy](/images/20_prerequisites/iam-2-attach-policy.png)

1. Click to create the new user:
[finish creation](/images/20_prerequisites/iam-3-create-user.png)

1. Take note of the login URL and save:
[login url](/images/20_prerequisites/iam-4-save-url.png)

1. Generate an SSH Key pair for the targeted AWS region. You can find the "Key Pairs" link in the left hand navigation under "Network & Security". 