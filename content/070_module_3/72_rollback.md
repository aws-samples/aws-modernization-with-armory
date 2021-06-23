---
title: "2. Rollback "
chapter: true
draft: false
weight: 42
---

## Rollback

The two key reasons why rollbacks are crucial are: consistency and available. Since modern applications are composed of many microservices, you need the ability to manage each microservice individually. For example in the update of a microservice application, many services might need to be updated at the same time. A failure or bug in one or more services can cause unexpected behavior in the application or cause it to completely fail. This is why rollback capability is so critical. It allows you to rollback an issue to a consistent state. 

In this section, you will walk through the steps for creating a pipeline that performs a rollback. The apple-app currently displays Banana. The rollback will revert the application to the previous version and you will now see Apple when you access the application. Armory Enterprise automatically versions and keeps track of your deployments. In this example, you can see that there are two historic versions of the deployment which you can see in the infrastructure section of the UI. Also, you will see a field called "Revisions Back". This field indicates how many versions to rollback. In this exercise, we can only rollback a single version.

1. Go to "Pipelines" screen and start creating a new pipeline
1. Give the pipeline the name `Rollback Apple`
2. Add stage and select the type "Undo Rollout (Manifest)"
3. Name it `Rollback Apple`
4. Choose Account "spinnaker"
5. Choose Namespace "dev"
6. Choose Kind "deployment"
7. Choose Name "apple-app"
8. Save Pipeline
9. Run the pipeline via manual execution
10. Once run, go back to the browser with the /apple appended to the ingress hostname and notice that the apple text has returned, no more banana. You have successfully rolled your deployment back to the previous version
![Rollback Pipeline](/images/armory-rollback-pipeline.png)
