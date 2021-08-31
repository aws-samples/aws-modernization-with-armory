---
title: "Review Pre-deployed Armory Solution"
chapter: false
weight: 11
---

Armory Solution is pre-installed for you on your AWS sandbox account you are currently in. 

Next steps:

1. Navigate to [CloudFormation Stacks](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks?filteringStatus=active&filteringText=&viewNested=true&hideStacks=false) where you can explore the installation and resources created
2. In Stacks, scroll down and find the parent stack with description `Armory installation`, select it
![Armory Installation](/images/armory-quick-start-stack.png)
3. Switch to **Outputs** tab. You should see *ArmoryUI* output parameter which is Armory Enterprise UI URL
![Armory Installation](/images/armory-quick-start-output.png)
