---
title: "Blue Green Deployment"
chapter: true
weight: 10

---
# Add manual judgment and wait stage and blue/green prod deployment

Next, we're going to show a blue/green deployment, which is handled by Spinnaker's traffic management capabilities.  We're going to gate this with both a manual judgment and a wait stage.

## Edit your pipeline:

1. Navigate to "Pipelines" in Armory Enterprise UI
   
1. Click on the "Configure" button next to your pipeline (or click on "Configure" in the top right, and select your pipeline)
   
1. Add the Manual Judgment Stage:
    - Click on the "Deploy Staging" stage
    - Click on "Add stage"
    - Select "Manual Judgment" from the "Type" dropdown
    - In the "Stage Name", enter `Manual Judgment: Deploy to Prod`
    - In the "Instructions" field, enter `Please verify Staging and click 'Continue' to deploy to Prod`
    - Click "Save Changes" in the bottom right.
    
1. Add the Wait Stage:
    - Click on the "Deploy Staging" stage
    - Click on "Add stage"
    - Select "Wait" from the "Type" dropdown
    - In the "Stage Name", enter `Wait 30 Seconds`
    - Click "Save Changes" in the bottom right.
{{% notice note %}}
Notice how we now have two stages that "Depend On" the "Deploy Staging" stage. Once the "Deploy Staging" stage finishes, both of these stages will start. A stage can have one or more stages that depend on it.
{{% /notice %}}
      ![Deploy Staging Dependencies](/images/armory-all-stages.png)

1. Now we're going to add the Kubernetes blue/green "Deploy Prod" stage
    - Click on the "Manual Judgment: Deploy to Prod" stage
    - Click on "Add Stage"
    - In the "Type" dropdown, select "Deploy (Manifest)"
    - Update the "Stage Name" field to be `Deploy Prod`
    - Click in the empty "Depends On" field, and select "Wait 30 Seconds".  
{{% notice note %}}
Notice how this stage depends on both the wait and manual judgment stages - it will wait till both are complete before it starts.  A stage can depend on one more or stages.
{{% /notice %}}
    - In the "Account" dropdown, select "Spinnaker"
    - Check the "Override Namespace" checkbox and select "prod" from the "Namespace" dropdown
      ![Prod Dependencies](/images/armory-prod-stage.png)
    - In the manifest field, copy and paste the below content:
      {{% notice %}}
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: hello-today
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: hello-today
      template:
        metadata:
          labels:
            app: hello-today
        spec:
          containers:
          - image: 'justinrlee/nginx:${parameters["tag"]}'
            name: primary
            ports:
            - containerPort: 80
              protocol: TCP
      {{% /notice %}}
{{% notice note %}}
Notice that this manifest is different from the other two manifests - this is explained below.
{{% /notice %}}
    - Below the manifest block, go to the "Rollout Strategy Options"
    - Check the box for "Spinnaker manages traffic based on your selected strategy"
    - Select "prod" from the "Service Namespace" dropdown
    - Select "hello-today" from the "Service(s)" dropdown
    - Check the "Send client requests to new pods" checkbox
    - Select ["Red/Black"](https://spinnaker.io/guides/user/kubernetes-v2/rollout-strategies/#redblack-rollouts) from the "Strategy" dropdown
    - Click "Save Changes" in the bottom right.
      ![Prod Rollout](/images/armory-prod-rollout.png)
    
## Then, trigger the pipeline:

1. Click back on the "Pipelines" tab at the top of the page
1. Click on "Start Manual Execution" next to your pipeline and specify some desired tag value
1. Click "Run"
1. Monitor execution and click "Continue" on first manual judgment stage after Deploy Dev
   ![Dev Manual Judgment](/images/armory-manual-judgment-1.png)
1. Wait a few seconds until "Deploy Staging" completed. Now you can see "Wait 30 Seconds" stage is also executing in parallel with "Manual Judgment: Deploy to Prod" stage, and "Deploy Prod" stage is waiting for both. Confirm manual judgment by clicking "Continue".
   ![Staging Manual Judgment and Wait Stages](/images/armory-manual-judgment-and-wait-stages.png)
1. Once "Deploy Prod" is completed you will see the following execution graph.
   ![Prod Deployment Completed](/images/armory-deploy-prod-completed.png)
1. Go to "Load Balancers", find Prod Ingress and it's URL, add "/prod/hello-today" and check your production deployment
   ![Hello Today](/images/armory-hello-today.png)

