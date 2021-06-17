---
title: "Reliable Deployments"
chapter: true
weight: 12
---
# So what is Continuous Delivery, Really? 

You don't want to be stuck in traffic. You want life to be simple, reliable, and in the case of deploying your applications, even, perhaps, dare I say, a little boring.

Let's take a little step back and think about how far things have come. We have gone from huge computers to ones not even visible by the eye. From huge server farms to virtual processing power and space up in the clouds. It follows that as things change and evolve, how you work with them needs to follow.

When we talk about continuous delivery, it is really boils down to the industry standard best practices for deploying your software.


- Blue/Green: An easy way to think about this is that it is similar to active-active high availability. You have two instances of your deployment running concurrently, the production build and a new one. Once you feel confident that the newer build is stable, traffic is shifted all at once from the old deployment to the new one. A configurable number of server groups are maintained, which allows for an easy rollback in case of issues. Variations of blue/green include:
 - Rolling Blue/Green: Similar to Blue/Green, but traffic is gradually shifted from the older deployment to the new one.
 - Highlander: Similar to Blue/Green, except the old deployment is destroyed once traffic is shifted.
- Canary: This consists of three instances: the current production instance, a baseline instance (a smaller clone of production), and a canary instance with the new deployment. The production instance handles most of the load while the baseline and canary each receive a smaller amount. After a predetermined amount of time, performance of the baseline and canary are compared. Whether the a deployment becomes the new production build depends on canary analysis that can be automated or manual.
- Automated rollbacks: Even with the best checks in place, things can happen. The most important thing is to be able to quickly react and avoid outages as well as pages to your on-call team.

Imagine it looking this simple...

![Pipelines](/images/pipelines.png)
 



 



