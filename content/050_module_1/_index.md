---
title: "Create Your First Pipeline"
chapter: true
weight: 5
---

## Module Overview

In Armory Enterprise, an "Application" is basically a grouping of the pipelines and resources deployed by those pipelines. An Application can group any set of related resources, and can group objects across multiple cloud targets (and cloud target types). Common ways to organize services are:

- One application for each microservice
- One application for a set of microservices that make up a single cohesive business function
- One application for each team

In this workshop, your will deploy a sample application into three different namespaces (dev, staging, prod). This involves creating the namespaces, load balancers, and ingresses for accessing the application. This module will walk you through creating a pipeline with two stages - dev and staging. The staging deployment will be gated with the manual judgement as example when you want to check your deployment first on dev environment. Also, you will be introduced to how the Spring Expression Language can be leveraged in a manifest when using Armory Enterprise.

We're going to create a demo pipeline that deploys to the Kubernetes cluster included with Armory Enterprise.

{{% notice note %}}
Note: this pipeline is a training exercise. Typically, you could configure Spinnaker to deploy to an external Kubernetes cluster where you want your application to live.
{{< /notice >}}

We will be deploying a "Hello Today" application that indicates the weekday on which it was deployed. Because we're deploying to EKS, we will use EKS built-in load balancing and ingress to navigate the following URL paths. 

- /dev/hello-today
- /staging/hello-today
- /prod/hello-today
 









































