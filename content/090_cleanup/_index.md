---
title: "Cleanup"
chapter: true
draft: false
weight: 90
---

# Workshop Cleanup

Congratulations on completing the workshop! Now although you may AWS credits to pay for the costs incurred today, the next few sections will instruct you how to turn off all the infrastructure you've created in order to work through the material.

Here is how to delete the stacks provisioned by CloudFormation:

1. Go to your AWS account and CloudFormation dashboard

1. Scroll to the parent Armory Quickstart stack **`Armory-Enterprise-on-EKS-New-VPC`** and select it
    ![CloudFormation Stack Delete](/images/cloudformation-stack-delete.png)

1. Press the Delete button
   ![CloudFormation Stack Delete Button](/images/cloudformation-stack-delete-button.png)
   
1. This process may take up to 30 minutes for everything to be fully deleted

1. Monitor the cleanup by selecting the events button.
    ![CloudFormation Stack Delete Monitor](/images/cloudformation-stack-delete-monitor.png)