---
title: "4. Create a New Pipeline"
chapter: true
weight: 12
---

# Create a New Pipeline

We're going to start off with a simple "Deploy Application" pipeline, that will have a single stage that deploys the dev version of our application. We're going to be deploying this as a Kubernetes Deployment object, which will handle rollouts for us.

Keep in mind that we have already created these resources:

- A dev Namespace
- A hello-today Service in the dev namespace
- A hello-today Ingress to expose the application on your Armory instance, on the /dev/hello-today endpoint
 
## Create the pipeline

Here's where need to start:

1. Log into the Armory Enterprise UI
2. Go to the "Applications" tab
3. Click on our "hello-today" application
4. Go to the "Pipelines" tab.

Then, actually create the pipeline:

1. In the top right, click the '+' icon (or "+ Create", depending on the size of your browser)
2. Give the pipeline the name "Deploy Application"
3. Add a 'tag' parameter:

      - Click "Add Parameter" (in the middle of the page)
      - Specify "tag" as the Name
      - Check the "Required" checkbox
      - Check the "Pin Parameter" checkbox
      - Add a Default Value of "monday" (all lowercase)
      
4. Add the Deploy Dev stage

      - "Add Stage"
      - In the "Type" dropdown, select "Deploy (Manifest)"
      - Update the "Stage Name" field to be "Deploy Dev"
      - In the "Account" dropdown, select "spinnaker"
      - Select the 'Override Namespace' checkbox, and select 'dev' in the dropdown
      - In the "Manifest" field, put this (note the ${parameters["tag"]} field, which will pull in the tag parameter)

<pre>
  <code>

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
   </code>
</pre>

5. Click "Save Changes"

Then, trigger the pipeline:

1. Click back on the "Pipelines" tab at the top of the page
2. Click on "Start Manual Execution" next to your newly created pipeline (you can also click "Start Manual Execution" in the top right, and then select your pipeline in the dropdown)
3. Click "Run"

Your application should be deployed. Look at the status of this in three ways:

- Go to the "Infrastructure" tab and "Clusters" subtab, and you should see your application, which consists of a Deployment with a single ReplicaSet. Examine different parts of this page.
- Go to the "Infrastructure" tab and "Load Balancers" subtab. Examine different parts of this page (for example, try checking the 'Instance' checkbox so you can see ReplicaSets and Pods attached to your Service)
- Go to https://<your-armory-ip-or-hostname>/dev/hello-today, and you should see your app.
