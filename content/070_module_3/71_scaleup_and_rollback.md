---
title: "1. Scale Up and Rollback"
chapter: true
draft: false
weight: 41
---
# Scale up and Rollback
<!--Add some context here-->

### Create pipeline "Deploy Apple"
1. Navigate to "Pipelines" and in the top right, click the '+ Create' icon (or "+", depending on the size of your browser)
1. Give the pipeline the name `Deploy Apple`
1. Click "Add Stage", select type "Deploy (Manifest)" and Stage Name is `Deploy Apple`
1. Under "Account" choose "spinnaker"
1. Check "Override Namespace" and select "dev" as the namespace
1. Copy and paste the following manifest YAML and click "Save Changes"
   {{% notice %}}
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
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: apple-service
    spec:
      selector:
        app: apple
      ports:
        - port: 5678 # Default port for image
    ---
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: example-ingress
      annotations:
        ingress.kubernetes.io/rewrite-target: /
    spec:
      rules:
      - http:
          paths:
            - path: /apple
              backend:
                serviceName: apple-service
                servicePort: 5678
    {{% /notice %}}
        
### Trigger pipeline and navigate to Apple app
1. Navigate to "Pipelines" screen and start  manual execution of "Deploy Apple" pipeline
1. Once completed visit "Load Balancers" screen and find the ingress of the apple deployment "ingress example-ingress" and select dev namespace. Then on the right side find Ingress URL. When clicking on the ingress, you should expect to get a 404. To access the apple app, you have to append */apple* to the end of the ingress URL. 
   
### Update pipeline to automatically update the version
Next we are going to update the YAML and Spinnaker is going to automatically update the version
<!--It's not clear version of app? We already did similar deployments for another pipeline-->

1. Click "Configure" on the "Deploy Apple" pipeline
1. Change the *'-text=apple'* under image for the deployment to *'-text=banana'* and save changes. Execute the pipeline
1. Doing so will create a new version of the deployment
1. Visit the ingress with the */apple* path appended and see that the app is now displaying the word *banana*.
