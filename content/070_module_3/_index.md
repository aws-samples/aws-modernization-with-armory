---
title: "Scale up and Rollback"
draft: false
weight: 7
---

In this section we will be scaling up and scaling down a ReplicaSet.\

A ReplicaSet is defined with fields, including a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a pod template specifying the data of new Pods it should create to meet the number of replicas criteria. A ReplicaSet then fulfills its purpose by creating and deleting Pods as needed to reach the desired number. When a ReplicaSet needs to create new Pods, it uses its Pod template.

In this module you will learn how to scale up a replicaset with Armory Enterprise and Rollback to previous versions.

The kubectl way to do this is to use the following:

`kubectl replace -f replcaset-definition.yml`
and
`kubectl scale --replicas=6 -f replicaset-definition.yml`



### replicaset-definition.yml
  {{% notice %}}
    #replicaset-definition.yml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: apple-app
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: apple
      template:
        metadata:
          labels:
            app: apple
            lb: apple
        spec:
          containers:
            - image: hashicorp/http-echo
              args:
               - "-text=apple"
              name: apple-app
     {{% /notice %}}

