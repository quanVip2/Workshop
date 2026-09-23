---
title: "Configuring Event Flows (Setting up S3 Event Notifications to Trigger Lambda)"
weight: 7
pre: " <b> 4.7 </b> "
---

## Objectives
Fully automate the image processing workflow by setting up an Event Trigger. Ensure that the moment an original image is uploaded by a user (via the Web interface) to the S3 Input bucket, the AWS Lambda function is immediately awakened to perform image compression and record the history into the database.

## Overview
The most powerful and elegant feature of an Event-driven Serverless Architecture is passive automation.

Instead of maintaining a virtual server running 24/7 just to continuously poll whether a new image file has been uploaded (which causes massive resource waste), we utilize the S3 Event Notifications feature. This feature allows the Amazon S3 bucket to act as a "watchman," proactively sending an activation signal (Trigger) directly to the AWS Lambda function as soon as a new file (Object) is created. As a result, the system achieves extremely low latency and zero operating costs when idle.

## Practice Content
This practice section includes two main procedures:

* Access the original image storage bucket (`kho-anh-goc-cua-toi-1`) to create an event notification workflow.
* Configure the triggering event type (`ObjectCreated`) and specify the destination as the image processing Lambda function.

## Expected Outcomes
* The `s3:ObjectCreated:*` event flow is successfully established on the S3 Input bucket.
* The S3 Input bucket and the AWS Lambda function are linked together into a seamless data pipeline.
* Any file placed into the Input bucket will automatically run through Lambda's Python source code without manual intervention.