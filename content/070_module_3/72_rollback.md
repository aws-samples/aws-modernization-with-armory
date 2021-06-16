---
title: "2. Rollback "
chapter: true
draft: false
weight: 42
---

## Rollback
1. In the top right, click the '+' icon (or "+ Create", depending on the size of your browser)
1. Give the pipeline the name "Rollback Apple"
2. Add Stage and select the type Undo Rollout (Manifest)
3. Name it Rollback Apple
4. Choose Account Spinnaker
5. Choose Namespace Dev
6. Choose Kind Deployment
7. Choose Name Apple-App
8. Save Pipeline
9. Run the pipeline via manual execution
10. Once run, go back to the browser with the /apple appended to the ingress hostname and notice that the apple text has returned, no more banana. You have succesfully rolled your deployment back to the previous version
