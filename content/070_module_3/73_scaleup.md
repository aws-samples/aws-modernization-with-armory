---
title: "3. Scaleup "
chapter: true
draft: false
weight: 42
---

To scale an application in Armory, you simply create a pipeline which is what you will do in this exercise. By now, you are an expert in creating pipelines in Armory Enterprise. You will be scaling the apple-app up to six replicas.  For "extra Points", ssh into the bastion host created by CloudFormation and use kubectl to confirm 6 Pods are running (kubectl get pods --namespace dev). Don't worry about installing or configuring kubectl. CloudFormation has done this work for you. 

## Scale Up
1. Go to the "Pipelines" screen and start creating a new pipeline
1. Give the pipeline the name `Scale up Apple`
2. Add stage and select the type "Scale (Manifest)"
3. Name it `Scale up Apple`
4. Choose Account "spinnaker"
5. Choose Namespace "dev"
6. Choose Kind "deployment"
7. For the Selector field,  select "Choose a static target"
8. Choose Name "apple-app"
9. For Replicas set 6
10. Save Pipeline and run the pipeline via manual execute
12. Switch to "Clusters" and find the "deployment apple-app". You can see the ReplicaSet and how it scaled up in the cluster section of the interface. You will now see 6 green bars under the apple-app deployment![Scale up ReplicaSet](/images/armory-scaleup-deployment.png)