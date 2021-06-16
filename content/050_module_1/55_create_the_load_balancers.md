---
title: "3. Create the Load Balancers"
chapter: true
weight: 12
---

## Create Load Balancers

Now that our Armory Application and Kubernetes Namespaces are created, we're going to set up some load balancers.

For each of our environments, we're going to set up two Kubernetes resources:

- A "Service" of type "ClusterIP", which acts as an internal load balancer to access our applications
- An "Ingress", which will configure Traefik to point specific paths on the Minnaker VM to our internal Services

Armory abstracts both Kubernetes Service and Kubernetes Ingress objects as Armory "Load Balancer" objects, so we'll be creating six total Armory "Load Balancers" (one Ingress and one Service for each of our three Namespaces).

Here's where need to start:

1. Log into the Armory Enterprise
2. Go to the "Applications" tab
3. Click on our "hello-today" application
4. Go to the "Infrastructure" tab and the "Load Balancers" subtab.
5. Then, we'll create our resources in batches of two.

Create the dev Service and Ingress

1. Click on "Create Load Balancer"
2. Paste in this:

<pre>
  <code>
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
  </code>
 </pre>

3. Click "Create"

4. Click "Close"

Create the prod Service and Ingress

1. Click on "Create Load Balancer"

2. Paste in this:

<pre>
  <code>
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
  </code>
 </pre>

3. Click "Create"

4. Click "Close"

You should now have six items on the "Load Balancers" page.

You could also create all six resources at once, or one at a time instead of two at a time.

Creation of the Service and Ingress could occur also occur through a Deploy (Manifest) pipeline stage that has the Service and Ingress resource manifests in it.
