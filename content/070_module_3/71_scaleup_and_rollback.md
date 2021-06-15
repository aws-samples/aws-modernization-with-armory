---
title: "1. Scale Up and Rollback"
chapter: true
draft: false
weight: 41
---
## Scaleup and Rollback
1. In the top right, click the '+' icon (or "+ Create", depending on the size of your browser)
1. Give the pipeline the name "Deploy Apple"
2. Click Add Stage and add a Deploy (Manifest) and Stage Name is Deploy Apple
3. Under Account Choose Spinnaker
4. Check Override Namespace
5. Choose dev as the namespace
6. And Copy in the following YAML and click Save

```
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
```

1. From Pipelines Screen click manual execution of Deploy Apple pipeline
2. Visit the ingress of the apple deployment by clicking on the Load balancer icon in the left pane, then on the right side click on the "example-ingress", which is in the status box. When clicking on the ingress, you should expect to get a 404, to access the apple app, you have to append the url path /apple to the end of the ingress. 
3. Next we are going to update the YAML and Spinnaker is going to automatically update the version
4. Click configure on the Deploy Apple Pipeline
5. Change the '-text=apple' under image for the deployment to '-text=banana' and run the 
6. Doing so will create a new version of the deployment
7. Visit the ingress with the /apple path appeneded and see that the app is now displaying the word banana.
