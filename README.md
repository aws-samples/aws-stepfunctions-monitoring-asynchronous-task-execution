# AWS Step Functions: Monitoring Asynchronous Task Execution

<!--BEGIN STABILITY BANNER-->
---

![Stability: Stable](https://img.shields.io/badge/stability-Stable-success.svg?style=for-the-badge)

> **This is a stable example. It should successfully build out of the box**
>
> This example uses core CloudFormation, and does not have any infrastructure requisites to build.

---
<!--END STABILITY BANNER-->


This example uses Lambda and CloudWatch Log subscription to publish custom CloudWatch Metrics for StepFunction execution SLA.

View the AWS blog post here: https://example.com/step-function-asynchronous-task-sla-monitoring


## Deploy
In CloudFormation console, create a stack using **step_functions_monitoring_template.yml** template. This can also be deployed using AWS CLI:
```
aws cloudformation deploy --template step_functions_monitoring_template.yml --stack-name <stack name>
```

After the deployment, you can locate the created workflow in resources section of the CloudFormation stack in AWS Console.

## Configuring SLA Alarms
After executing the workflow, SLA metrics will be published into custom metrics namespace under **TaskMetrics**. Create a custom alarm with a desired threshold.
In this example execution times range 3 - 20 seconds, therefore for demonstration purposes threshold in 10 - 18 second range is suggested.

## The Component Structure
This example contains:
* Lambda functions to handle processing logic
* StepFunction workflow to orchestrate a business process in asynchronous manner
* SQS queue used to facilitate asynchronous callback whenever processing completes
* Log subscription used as a source of custom execution telemetry used to publish SLA metrics
