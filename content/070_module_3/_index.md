---
title: "Scale up and Rollback"
draft: false
weight: 7
---

In this section we will be scaling up and scaling down a ReplicaSet.

A key capability and benefit of a modern distributed system is the ability to right size and immediately adjust your infrastructure to meet the demands of your business.  Another critical benefit is the ability to rollback changes to an application in production when trouble is detected.  The combination of Kubernetes and Armory Enterprise allow you to do this quickly and at scale.

In this exercise, you will be introduced to scaling up and scaling down an application, as well as, how to roll back an application to a previous version.  In Kubernetes, we look at a Pod as the artifact containing the application and is the abstraction that is monitored and managed to keep your application available and scaled. Another abstraction in Kubernetes that works to keep your Pods available is called a Replicaset. A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. 

A ReplicaSet is defined with fields, including a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a pod template specifying the data of new Pods it should create to meet the number of replicas criteria. A ReplicaSet then fulfills its purpose by creating and deleting Pods as needed to reach the desired number. When a ReplicaSet needs to create new Pods, it uses its Pod template.

Using Armory Enterprise, you simply need to click on a field to scale up and down the number of pods to meet the demand. For rolling back an application, you will create a new pipeline.:

1. Create a pipeline and deploy an application.
2. From the Armory UI, you will scale up and down the application.
2. Next, you update and deploy a new version of the application
3. Finally, you will roll back to the previous version.



![Scale Up](/images/rollback.png)
