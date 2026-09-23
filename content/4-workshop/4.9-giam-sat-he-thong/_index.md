---
title: "System Monitoring (Checking CloudWatch Logs and Performance Measurement)"
weight: 9
pre: " <b> 4.9 </b> "
---

## Objectives
Monitor the background operations of the image processing system, measure actual execution time (`Duration`), memory consumption (`Max Memory Used`), and analyze errors (if any) via the Amazon CloudWatch service.

## Overview
In a Serverless architecture, you do not have direct access to the underlying operating system to view console screens or traditional log files. Therefore, Amazon CloudWatch acts as the single most powerful "eye" for monitoring the system.

Thanks to attaching the `AWSLambdaBasicExecutionRole` permission in Chapter 5.4, every time the AWS Lambda function runs, it automatically pushes all `print()` statement outputs and measurement metrics to CloudWatch. Understanding these metrics helps us evaluate whether the 512MB RAM and 15-second Timeout configuration is truly optimal, thereby meeting the project's testing and measurement criteria.

## Practice Content
This practice section includes two main procedures:

* Navigate from the AWS Lambda function interface to Amazon CloudWatch Log Groups.
* Read the log stream data to analyze the `REPORT` metrics regarding memory and time.

## Expected Outcomes
* Know how to retrieve the activity logs of any Lambda function.
* Understand the core parameters within the CloudWatch `REPORT` line.
* Confirm how much actual RAM image compression using Pillow consumes, thereby proving that the decision to upgrade RAM from 128MB to 512MB has solid technical grounds.