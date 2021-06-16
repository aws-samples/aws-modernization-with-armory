---
title: "3. Scaleup "
chapter: true
draft: false
weight: 42
---

## Scale Up
1. In the top right, click the '+' icon (or "+ Create", depending on the size of your browser)
1. Give the pipeline the name "Scaleup Apple"
2. Add Stage and select the type Scale (Manifest)
3. Name it Scaleup Apple
4. Choose Account Spinnaker
5. Choose Namespace Dev
6. Choose Kind Deployment
7. Selector choose static target
8. Choose Name Apple-App
9. Replicas choose 6
10. Save Pipeline
11. Run the pipeline via manual execute
12. Go see the replicaset and how it scaled up in the Cluster section of the interface. You will now see 6 green bars under the Apple App Deployment
