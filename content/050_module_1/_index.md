---
title: "Create Your First Pipeline"
chapter: false
weight: 5
---

We're going to create a demo pipeline that deploys to the Kubernetes cluster included with Armory Enterprise.

We will be deploying a Hello World application that indicates the weekday on which it was deployed.

Note: this pipeline is a training exercise. Typically, you could configure Spinnaker to deploy to some external Kubernetes cluster where you want your application to live.

Because we're deploying to EKS, we will use EKS builtin load balancing and ingress to navigate the following URL paths. 

- /dev/hello-today
- /stage/hello-today
- /prod/hello-today
 









































