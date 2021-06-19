---
title: "3. Scaleup "
chapter: true
draft: false
weight: 42
---

## Scale Up
1. Go to "Pipelines" screen and start creating a new pipeline
1. Give the pipeline the name `Scale up Apple`
2. Add stage and select the type "Scale (Manifest)"
3. Name it `Scale up Apple`
4. Choose Account "spinnaker"
5. Choose Namespace "dev"
6. Choose Kind "deployment"
7. For Selector select "Choose a static target"
8. Choose Name "apple-app"
9. For Replicas set 6
10. Save Pipeline and run the pipeline via manual execute
12. Switch to "Clusters" and find "deployment apple-app". You can see the ReplicaSet and how it scaled up in the cluster section of the interface. You will now see 6 green bars under the apple-app deployment![Scale up ReplicaSet](/images/armory-scaleup-deployment.png)