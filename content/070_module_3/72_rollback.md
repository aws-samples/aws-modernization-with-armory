---
title: "2. Rollback "
chapter: true
draft: false
weight: 42
---

## Rollback
1. Go to "Pipelines" screen and start creating a new pipeline
1. Give the pipeline the name `Rollback Apple`
2. Add stage and select the type "Undo Rollout (Manifest)"
3. Name it `Rollback Apple`
4. Choose Account "spinnaker"
5. Choose Namespace "dev"
6. Choose Kind "deployment"
7. Choose Name "apple-app"
8. Save Pipeline
9. Run the pipeline via manual execution
10. Once run, go back to the browser with the /apple appended to the ingress hostname and notice that the apple text has returned, no more banana. You have successfully rolled your deployment back to the previous version
![Rollback Pipeline](/images/armory-rollback-pipeline.png)