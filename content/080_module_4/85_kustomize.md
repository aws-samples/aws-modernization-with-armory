---
title: "6. Kustomize"
chapter: true
weight: 10
---
## Kustomize

https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/

**Why use Kustomize patches for Spinnaker configuration**
Even though you can configure Armory Enterprise or Spinnaker in a single manifest file, the advantage of using [Kustomize](https://kustomize.io/) patch files is **readability, consistency across environments, and maintainability.**


**How Kustomize works**
Kustomize uses patch files to build a deployment file by overwriting sections of the `spinnakerservice.yml` manifest file. You declare your patch files in a `kustomization.yml` file, which `kubectl` and Kustomize and use to build the Armory Enterprise or Spinnaker manifest file.
You can put each manifest config section in its own file. For example, if you create a `profiles-patch.yml` patch with configuration for various services, you are telling Kustomize to overwrite the `profiles` section of the `spinnakerservice.yml` manifest with the contents of `profiles-patch.yml`. Kustomize is flexible, though, so you could instead create a separate patch file for each service (`profiles-clouddriver-patch.yml`, `profiles-gate-patch.yml`, `profiles-deck-patch.yml`, etc.), and then declare those patches in the `kustomization.yml` file.
Kustomize is part of `kubectl`, so you do not need to install Kustomize locally to build and verify your manifest file. You can run `kubectl kustomize <path-to-kustomization.yml>`. This prints out the contents of the manifest file that Kustomize builds using your `kustomization.yml` file.


> `kubectl` versions up to and including v1.20 come bundled with Kustomize v2.0.3. `kubectl` 1.21 comes bundled with Kustomize v4.0.5. Using Kustomize patches has been tested with `kubectl` v1.19.x. and standalone Kustomize v2 and v3. You may see a `panic` error if you use the `spinnaker-kustomize-patches` repo with Kustomize v4.0+ or `kubectl` v1.21+.


## Spinnaker Kustomize patches repo

Armory maintains the `spinnakaker-kustomize-patches` [repo](https://github.com/armory/spinnaker-kustomize-patches), which contains common configuration options for Armory Enterprise or Spinnaker as well as helper scripts. The patches in this repo give you a reliable starting point when adding and removing features.

> All of the patches in the repo are for configuring Armory Enterprise. To use the patches to configure open source Spinnaker, you must change `spinnaker.armory.io` in the `apiVersion` field to `spinnaker.io`. This field is on the first line in a patch file.

To start, create your own copy of the `spinnaker-kustomize-patches` repository by clicking the `Use this template` button:

![button](https://d33wubrfki0l68.cloudfront.net/5ec6086e2acf30a9f12111a354c89fc7dfc25afc/2fabf/images/kustomize-patches-repo-clone.png)

> If you intend to update your copy from upstream, use **Fork** instead. See [Creating a repository from a template](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) for the difference between **Use this template** and **Fork**.

Once created, clone this repository to your local machine.


## Configure Armory Enterprise

Follow these steps to configure Armory Enterprise:

1. [Choose a](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#choose-a-kustomization-file) `[kustomization.yml](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#choose-a-kustomization-file)` [file](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#choose-a-kustomization-file).
2. (Optional) If you are deploying open source Spinnaker, [change the](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#change-the-apiversion) `[apiVersion](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#change-the-apiversion)` [in each patch file](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#change-the-apiversion).
3. [Set the Armory Enterprise (or Spinnaker) version](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#set-the-spinnaker-version).
4. [Verify the content of each resource file](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#verify-resources).
5. [Verify the configuration contents of each patch file](https://docs.armory.io/docs/installation/armory-operator/op-config-kustomize/#verify-patches).

**Set the Armory Enterprise version**
In `spinnaker-kustomize-patches/core_config/patch-version.yml`, set the [Armory Enterprise version](https://docs.armory.io/docs/release-notes/rn-armory-spinnaker/) or [Spinnaker version](https://spinnaker.io/community/releases/versions/) that you want to deploy, such as `2.26.0` (Armory Enterprise) or `1.25.3` (Spinnaker).

    kind: SpinnakerService
    metadata:
      name: spinnaker
    spec:
      spinnakerConfig:
        # ------- Main config section, equivalent to "~/.hal/config" from Halyard
        config:
          version: 2.26.0
     

Copy
Add `core_config/patch-version.yml` to your `kustomization.yml` file in the `patchesStrategicMerge` section.



## Deploy Armory Enterprise

Once you have configured your patch files, you can deploy Armory Enterprise.

1. Create the `spinnaker` namespace:
    kubectl create ns spinnaker
2. Copy
3. If you want to use a different namespace, you must update the `namespace` value in your `kustomization.yml` file.
4. (Optional) Verify the Kustomize build output:
    kubectl kustomize <path-to-kustomization.yml>
5. Copy
6. This prints out the contents of the manifest file that Kustomize built based on your `kustomization.yml` file.
7. Apply the manifest:
    kubectl apply -k <path-to-kustomization.yml>
8. Copy
9. Watch the install progress and see the pods being created:
    kubectl -n spinnaker get spinsvc spinnaker -w




