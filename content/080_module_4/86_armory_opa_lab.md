---
title: "7. Armory OPA Lab"
chapter: true
weight: 10
---

## Delete Spinnaker
    kubectl delete ns spinnaker


## Create NameSpace Spinnaker
    kubectl create ns spinnaker


## Download kubectl command 
    curl -LO https://dl.k8s.io/release/v1.19.0/bin/linux/amd64/kubectl
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

## Chmod +x kubectl command
    chmod +x kubectl


## Create secrets
    cd spinnaker-kustomize-patches/secrets; ./create-secrets.sh



## Edit kustomization.yml
    configMapGenerator:
      # ConfigMap holding OPA policy definitions to use by Armory's policy engine. Required by patch-policyengine.yml
      - name: spin-policies
        files:
          - armory/policies/manual-judgement.rego


## Run kustomize
    ~/kubectl apply -k /home/ec2-user/spinnaker-kustomize-patches


## Watch for Pods to Come Up
    watch kubectl get pods -n spinnaker


## Get Spin Deck URL
    kubectl get svc spin-deck -n spinnaker 
----------
## OPA

OPA Rules/Policies


    kubectl -n <opaServerNamespace> create configmap manual-judgment --from-file=manual-judgment.rego


    kubectl -n <opaServerNamespace> label configmap manual-judgment openpolicyagent.org/policy=rego


## Go over policy engine Example Policies

https://docs.armory.io/docs/armory-admin/policy-engine/policy-engine-use/example-policies/


