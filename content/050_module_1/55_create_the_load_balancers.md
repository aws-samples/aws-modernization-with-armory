---
title: "2. Create the Load Balancers"
chapter: true
weight: 12
---

## Create Load Balancers

Now that our Armory Application and Kubernetes Namespaces are created, we're going to set up some load balancers.

For each of our environments, we're going to set up two Kubernetes resources:

- A "Service" of type "ClusterIP", which acts as an internal load balancer to access our applications
- An "Ingress", which acts as an external entry will route the requests to the appropriate backend services

To learn more about Ingress, and why its important, check out the Kubernetes [documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/). 

Armory abstracts both Kubernetes Service and Kubernetes Ingress objects as Armory "Load Balancer" objects, so we'll be creating six total Armory "Load Balancers" (one Ingress and one Service for each of our three Namespaces).


![Ingress](/images/ingress.png)


### Create the "dev" Service and Ingress

1. In our Hello Today application in Armory Enterprise UI choose "Load Balancers" on the left-hand bar
1. Click "Create Load Balancer"
1. Copy and paste the manifest content below, click "Create". It will take a few second to deploy it and you can click "Close" now

<pre><code>
apiVersion: v1
kind: Namespace
metadata:
  name: dev
---
apiVersion: v1
kind: Service
metadata:
  name: hello-today
  namespace: dev
spec:
  ports:
    - name: http
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    lb: hello-today
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    traefik.ingress.kubernetes.io/rule-type: PathPrefixStrip
    nginx.ingress.kubernetes.io/rewrite-target: /
  labels:
    app: hello-today
  name: hello-today
  namespace: dev
spec:
  rules:
    - http:
        paths:
          - backend:
              serviceName: hello-today
              servicePort: http
            path: /dev/hello-today
</code></pre>

### Create the "staging" Service and Ingress

1. Click "Create Load Balancer"
1. Copy and paste the manifest content below, click "Create". It will take a few second to deploy it and you can click "Close" now

<pre><code>
apiVersion: v1
kind: Namespace
metadata:
  name: staging
---
apiVersion: v1
kind: Service
metadata:
  name: hello-today
  namespace: staging
spec:
  ports:
    - name: http
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    lb: hello-today
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    traefik.ingress.kubernetes.io/rule-type: PathPrefixStrip
    nginx.ingress.kubernetes.io/rewrite-target: /
  labels:
    app: hello-today
  name: hello-today
  namespace: staging
spec:
  rules:
    - http:
        paths:
          - backend:
              serviceName: hello-today
              servicePort: http
            path: /staging/hello-today
</code></pre>

### Create the prod Service and Ingress

1. Click "Create Load Balancer"
1. Copy and paste the manifest content below, click "Create". It will take a few second to deploy it and you can click "Close" now

<pre><code>
apiVersion: v1
kind: Namespace
metadata:
      name: prod
---
apiVersion: v1
kind: Service
metadata:
      name: hello-today
      namespace: prod
spec:
      ports:
        - name: http
          port: 80
          protocol: TCP
          targetPort: 80
      selector:
        lb: hello-today
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
      annotations:
        traefik.ingress.kubernetes.io/rule-type: PathPrefixStrip
        nginx.ingress.kubernetes.io/rewrite-target: /
      labels:
        app: hello-today
      name: hello-today
      namespace: prod
spec:
      rules:
        - http:
            paths:
              - backend:
                  serviceName: hello-today
                  servicePort: http
                path: /prod/hello-today
</code></pre>

It takes a few seconds to finalize manifest deployment. Refresh the page and you should now have six items on the "Load Balancers" page. You also can create all six resources at once, or one at a time instead of two at a time via configuration above.
![Load Balancers](/images/armory-load-balancers.png)

Creation of the Service and Ingress could also occur through a Deploy (Manifest) pipeline stage that has the Service and Ingress resource manifests in it.
