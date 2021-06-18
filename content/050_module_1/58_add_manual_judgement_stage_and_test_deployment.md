---
title: "5. Add Manual Judgment"
chapter: true
weight: 18
---

# Expand the pipeline: Add manual judgment and test deployment

Now that we have a running pipelines, let's add a promotion to a higher environment, gated by a manual approval. Navigate to "Pipelines" in Armory Enterprise UI.

### Edit your pipeline

1. Click on the "Configure" button next to your pipeline (or click on "Configure" in the top right, and select your pipeline)
1. Click on the "Configuration" icon on the left side of the pipeline
1. Add the "Manual Judgment: Deploy to Stage"
    - Click "Add stage". Note how the stage is set to run at the beginning of the pipeline
    - Select "Manual Judgment" from the "Type" dropdown
    - In the "Stage Name", enter "Manual Judgment: Deploy to Test"
    - In the "Instructions" field, enter "Please verify Dev and click 'Continue' to continue deploying to Test"
    - Click in the "Depends On" field at the top, and select your "Deploy Dev" stage. Notice how this rearranges the stages so that the manual judgment stage depends on (starts after) the dev deployment stage
    - Click "Save Changes" in the bottom right
1. Add the Deploy Test stage
   - In the pipeline layout section at the top of the page, click on "Manual Judgment: Deploy to Test" (you're probably already here)
   - Click "Add stage". Notice how the stage is dependent on the stage you had selected when you added the stage (the manual judgment stage).
   - In the "Type" dropdown, select "Deploy (Manifest)"
   - Update the "Stage Name" field to be "Deploy Test"
   - In the "Account" dropdown, select "spinnaker"
   - Select the 'Override Namespace' checkbox, and select 'test' in the dropdown
   - In the "Manifest" field, put this (note the ${parameters["tag"]} field, which will pull in the tag parameter). Click "Save Changes"

<pre><code>
apiVersion: apps/v1
kind: Deployment
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
        lb: hello-today
    spec:
      containers:
        - image: 'justinrlee/nginx:${parameters["tag"]}'
          name: primary
          ports:
            - containerPort: 80
</code></pre>


### Trigger the pipeline

1. Click back on the "Pipelines" tab at the top of the page
2. Click on "Start Manual Execution" next to your newly created pipeline (you can also click "Start Manual Execution" in the top right, and then select your pipeline in the dropdown)
3. Click "Run"

Notice that we used the exact same manifest; we just selected a different override namespace. This works because the manifest doesn't have hardcoded namespaces.

Right now, we only have one Kubernetes "Account", called "spinnaker", which refers to the Kubernetes cluster that Armory Enterprise is running on.

If we have added additional Kubernetes clusters to Armory, we could also (alternately or in addition) configure Armory to deploy to a different Kubernetes cluster by selecting a different option in the "Account" dropdown.

