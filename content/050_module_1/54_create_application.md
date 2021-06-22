---
title: "1. Create the Application"
chapter: true
weight: 12
---

# Create the Application


Let's create an application called "hello-today". Since we are deploying to a kubernetes cluster, we need to enter information about the application which is stored in a yaml file. Note, you will be pasting the yaml into the appropriate location in the UI.  You will be creating a pipeline that will be used to deploy the appliction. The pipeline will include creating a load balancer and a manual judgement stage. 

1. Open the browser and use the link you specified in the Setup section.  
1. Click on "Applications" in Armory Enterprise UI you have opened after setup step
1. Click "Create Application"
1. Name the application `hello-today` and put in your email address in the "Owner Email" field
1. Choose Repo Type
1. Click "Create"

![New Application](/images/create-armory-application.png)

Now you can go back to "Applications" page (click Refresh if needed) and you should be able to see you new application created.
