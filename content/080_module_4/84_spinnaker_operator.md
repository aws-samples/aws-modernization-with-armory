---
title: "5. Spinnaker Operator"
chapter: true
weight: 10
---

## Spinnaker Operator

https://docs.armory.io/docs/installation/armory-operator/

**What are Kubernetes Operators for Spinnaker?**

- The **Armory Operator**  extends the Spinnaker Operator’s features by providing the ability to configure Armory Enterprise’s [features](https://docs.armory.io/docs/#what-is-armory-enterprise), such as Pipelines as Code and Policy Engine. The Armory Operator and Armory Enterprise are closed source and not free to use.


- The **Spinnaker Operator** is a Kubernetes controller for deploying and managing Spinnaker. The Spinnaker Operator and Spinnaker are both open source and free to use.

**Advantages of using the operator for an Armory installation**

- Use a Kubernetes manifest to deploy and manage Armory Enterprise or Spinnaker.
- Use `kubectl` to deploy, manage, and access Armory Enterprise or Spinnaker like you would with any other app deployed on Kubernetes.
- Store and reference configuration secrets in one of the [supported secrets engines](https://docs.armory.io/docs/armory-admin/secrets/).
- Store your configuration in `git` for an auditable and reversible GitOps workflow.

