---
title: "Module 4: DevSecOps and Compliance pipelines"
chapter: true
weight: 7
---

## DevSecOps Introduction

DevSecOps stands for development, security, and operations. It's an approach to culture, automation, and platform design that integrates security as a shared responsibility throughout the entire IT lifecycle. As the move to cloud-native applications and services has accelerated, concerns about better securing these new applications and the underlying infrastructure have also grown. Workloads are temporary. Traditional security tools often don’t work for cloud-native technologies. Security needs to be declarative, built-in, and automated. Apps need to be natively more secure. Security needs to shift left in the application life cycle.

DevSecOps means thinking about application and infrastructure security from the start. It also means automating some security gates to keep the DevOps workflow from slowing down. Selecting the right tools to continuously integrate security, like agreeing on an integrated Continuous Integration/Continuous Delivery (CI/CD) approach with security features, can help meet these goals. However, effective DevOps security requires more than new tools—it builds on the cultural changes of DevOps to integrate the work of security teams sooner rather than later.

DevOps is a combination of cultural philosophies, practices, and tools that emphasizes collaboration and communication between software developers and IT infrastructure teams while automating an organization’s ability to deliver applications and services rapidly, frequently, and more reliably.

CI/CD stands for continuous integration and continuous deployment. These concepts represent everything related to automation of application development and the deployment pipeline — from the moment a developer adds a change to a central repository until that code winds up in production.

DevSecOps covers security of and in the CI/CD pipeline, including automating security operations and auditing. The goals of DevSecOps are to:

- Embed security knowledge into DevOps teams so that they can secure the pipelines they design and automate.
- Embed application development knowledge and automated tools and processes into security teams so that they can provide security at scale in the cloud.

A great way to embed DevSecOps into the CI/CD pipeline is to configure Armory Enterprise to use OPA. OPA is a general-purpose policy engine that makes policy a first-class citizen within the cloud-native ecosystem, putting it on par with servers, networks, and storage. Its uses range from authorization and admission control to data filtering. In short, OPA provides unified, context-aware policy controls for cloud-native environments. OPA policy is context-aware, meaning that the administrator can make policy decisions based on what is happening in the real world, such as:

- Is there currently an outage?
- Is there a new vulnerability that’s been released?
- Who are the people on call right now?
