---
title: "3. Create a New Pipeline"
chapter: true
weight: 12
---

# Create a New Pipeline

We're going to start off with a simple "Deploy Application" pipeline, that will have a single stage that deploys the dev version of our application. We're going to be deploying this as a Kubernetes Deployment object, which will handle rollouts for us.

### Create the pipeline

1. Switch to "Pipelines" tab on the left-hand bar
   
1. Choose "Configure a new pipeline" if it is your first pipeline (otherwise you should see "+ Create" button)
   
1. Give the pipeline the name `Deploy Application`
   
1. Add a 'tag' parameter:
      - Click "Add Parameter" (in the middle of the page)
      - Specify `tag` as the Name
      - Check the "Required" checkbox
      - Check the "Pin Parameter" checkbox
      - Add a Default Value of `monday` (all lowercase)
        ![Add Pipeline parameter](/images/armory-create-pipeline-parameter.png)
        
1. Add the Deploy Dev stage
      - Click "Add Stage" at the top section of the configuration
      - In the "Type" dropdown, select `Deploy (Manifest)`
      - Update the "Stage Name" field to be `Deploy Dev`
      - In the "Account" dropdown, select "spinnaker"
      - Select the 'Override Namespace' checkbox, and select 'dev' in the dropdown
      - Copy and paste the manifest content below. Note the *${parameters["tag"]}* field, which will pull in the tag parameter defined above. Click "Save Changes" now.
   
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

![Create Pipeline](/images/armory-create-deploy-pipeline.png)

### Trigger the pipeline

1. Click back on the "Pipelines" tab at the top of the page
1. Click on "Start Manual Execution" next to your newly created pipeline (you can also click "Start Manual Execution" in the top right, and then select your pipeline in the dropdown)
   ![Create Pipeline](/images/armory-pipeline-start.png)
1. Click "Run"


Your application should be deployed. Look at the status of this in three ways:

- Go to the left-hand infrastructure tab and choose "Clusters". You should see your application, which consists of a Deployment with a single ReplicaSet. Examine different parts of this page
  ![Create Pipeline](/images/armory-clusters.png)
- Go to the "Load Balancers". Examine different parts of this page (for example, try checking the 'Instance' checkbox so you can see ReplicaSets and Pods attached to your Service)
  ![Create Pipeline](/images/armory-load-balancers-with-resources.png)
- Navigate to "Load Balancers", select DEV namespace in "ingress hello-today" and on the right-hand information tab you can identify Ingress URL. Replace it in https://\<your-ingresss-url\>/dev/hello-today, and you should see your app returning last deployed tag value
  ![Ingress Address](/images/armory-ingress-info.png)
