---
title: "EC2 Key Pair"
chapter: true
weight: 11
---

## Generating SSH Key Pair for EC2
An EC2 Key Pair allows users to securely access into an EC2 instance. For more information, visit the [EC2 Key Pair documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html). Follow the below steps on how to create your own!
   
1. Navigate to your [EC2 Home](https://us-east-1.console.aws.amazon.com/ec2/v2/home?region=us-east-1#Home:)

1. Find the "Key Pairs" link in the left-hand navigation under "Network & Security".
   ![EC2 Key Pair Menu](/images/keypair-menu.png)
   
1. Create one if you do not have any.  Keep the file format as the default PEM.
   ![Create SSH Pair](/images/ec2-ssh-keypair.png)
   
Awesome! You've created an EC2 key pair, you will need it as the parameter for Armory QuickStart (for Bastion host access).