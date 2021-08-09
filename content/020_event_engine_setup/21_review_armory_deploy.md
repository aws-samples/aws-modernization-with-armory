---
title: "Review Pre-deployed Armory Solution"
chapter: false
weight: 11
---

Armory Solution is pre-installed for you on your AWS sandbox account you are currently in. You can navigate to CloudFormation to explore the installation.

Next steps:

1. Navigate to [EC2 Dashboard, running instances](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:instanceState=running) and select the Bastion host, it is an EC2 instance with the name *EKSBastion*
   
1. Connect to EKSBastion (choose *Connect* option in the menu on the top left). New terminal window will be opened in the browser page
   
1. In AWS Management Console, navigate to [EKS Clusters](https://us-east-2.console.aws.amazon.com/eks/home?region=us-east-2#/clusters) and check for EKS Cluster name, copy the name and use in the next command

1. Update AWS config with the region and EKS Cluster name by executing (replace *EKS_Cluster_Name* with real name captured from the EKS Clusters list). You will see information about new context added to the config
   `aws eks --region us-east-2 update-kubeconfig --name EKS_Cluster_Name`
   
1. Get External IP for the UI we will be using in the next steps. Copy the IP address and go to the browser, you can open Armory Enterprise UI by navigating to https://(External IP):9000
   `kubectl get service/spin-deck -n spinnaker`
   
Your URL should look similar to:
https://a3a20f8a6418d4daa8146df2902b90ec-1185297719.us-east-2.elb.amazonaws.com:9000