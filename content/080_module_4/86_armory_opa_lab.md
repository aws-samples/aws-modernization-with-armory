---
title: "Armory OPA Lab"
chapter: false
weight: 60
---

In this lab we will install Armory Enterprise with OPA (Open Policy Agent). 
We will configure OPA to prevent the creation of pipelines without at least 
one manual judgment step. 

If a pipeline doesn't have at least one manual judgment step, the pipeline will 
not be able to be saved. 

This manual judgment OPA logic is a basic "hello world" style example. After creating
this configuration we will go through examples of more complex OPA logic and will choose interesting
ones to try out together. 

#### 1. Delete Namespace Spinnaker
    kubectl delete ns spinnaker

#### 2. Create Namespace Spinnaker
    kubectl create ns spinnaker

#### 3. Download [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) command 
    curl -LO https://dl.k8s.io/release/v1.19.0/bin/linux/amd64/kubectl

#### 4. Chmod +x kubectl command
    chmod +x kubectl

#### 5. Create secrets
    cd spinnaker-kustomize-patches/secrets; ./create-secrets.sh

#### 6. Edit kustomization.yml
    configMapGenerator:
      # ConfigMap holding OPA policy definitions to use by Armory's policy engine. Required by patch-policyengine.yml
      - name: spin-policies
        files:
          - armory/policies/manual-judgement.rego

#### 7. Edit the spin-policies config map
	remove the 1 := 0, it is a rego null value

#### 8. Run kustomize
    ~/kubectl apply -k /home/ec2-user/spinnaker-kustomize-patches

#### 9. Watch for Pods to Come Up
    watch kubectl get pods -n spinnaker

#### 10. Get Spin Deck URL
    kubectl get svc spin-deck -n spinnaker 

----------

## Verify

Now you can test it, Armory's engine would not allow any application without Manual Judgement step.

1. Create an application in your spinnaker installation

2. Create a pipeline in your application

3. Try to save a pipeline without a manual judgment

4. Notice that the pipeline can not be saved due to the Open Policy Agent preventing it.

----------
## OPA

OPA Rules/Policies


    kubectl -n spinnaker create configmap manual-judgment --from-file=manual-judgment.rego


    kubectl -n spinnaker label configmap manual-judgment openpolicyagent.org/policy=rego


## Go over policy engine Example Policies

https://docs.armory.io/docs/armory-admin/policy-engine/policy-engine-use/example-policies/


