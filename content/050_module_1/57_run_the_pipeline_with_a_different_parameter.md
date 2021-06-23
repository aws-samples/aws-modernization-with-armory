---
title: "4. Run the Pipeline with a Different Parameter"
chapter: true
weight: 12
---

# Run the Pipeline with a Different Parameter

In the "Creating a New Pipeline" section, step 5, you copied yaml that had a tag parameter entry. The tag paramter is implemented as a pipeline expression. Pipeline expressions allow you to dynamically set and access variables during pipeline execution. You can use an expression in almost any text field in a Armory Enterprise pipeline stage. Pipeline expressions help you use arbitrary values about the state of your system in the execution of your pipelines. You can use them to turn on or off particular stages or branches of your pipeline, dynamically name your stack, check the status of another stage, and perform other operations, or pass a value to your application .

What this dynamic configuration possible is Armory Enterprises SpEL (Spring Expression Language). The Spring Expression Language (SpEL for short) is a powerful expression language that supports querying and manipulating an object graph at runtime. The language syntax is similar to Unified EL but offers additional features, most notably method invocation and basic string templating functionality. For more information please refer to Armory's SpEL [documentation](https://docs.armory.io/docs/spinnaker-user-guides/expression-language/).

1. Click back on the "Pipelines" tab at the top of the page
1. Click on "Start Manual Execution" next to your newly created pipeline (you can also click "Start Manual  
Execution" in the top right, and then select your pipeline in the dropdown)
1. Replace "monday" with some other day of the week (like 'tuesday' or 'wednesday')
1. Click "Run"
1. Refresh you dev application page to see the updated value
