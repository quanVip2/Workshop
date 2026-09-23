---
title: "Processing Logic Implementation"
weight: 5
pre: " <b> 4.6 </b> "
---

## Objectives
Build the "brain" of the image processing system using a Serverless Compute service. Ensure the AWS Lambda function is configured correctly with the Python 3.12 environment, successfully integrates the Pillow graphics library via Lambda Layer, allocates sufficient RAM/Timeout resources, and successfully deploys the processing source code.

## Overview
AWS Lambda acts as the central processing core in the Event-driven model. When a new image is uploaded to S3, Lambda is awakened to perform its tasks.

However, the default Python environment in Lambda is highly streamlined and does not come with built-in graphics processing libraries (like PIL/Pillow). Instead of packaging the source code and libraries into a complex ZIP file (which is prone to environment compatibility errors between Windows and Linux), this workshop applies the Lambda Layers solution by utilizing the Klayers open-source repository to directly "embed" the Pillow library into the function. Additionally, graphics processing requires significant computational power, so fine-tuning the Memory (RAM) and Timeout parameters is mandatory to prevent the system from crashing.

## Practice Content
This practice section includes three main procedures:

* Initialize the AWS Lambda function and attach the IAM Role created in the previous section.
* Configure the Lambda Layer (Pillow) compatible with the Python 3.12 environment in the `us-east-1` region.
* Update the Python source code, configure system resources (512MB RAM, 15s Timeout), and Deploy.

## Expected Outcomes
* The Lambda function is successfully initialized with the Python 3.12 Runtime.
* The Pillow library is successfully added via ARN specification without encountering the "The resource you requested does not exist" error.
* The image compression source code (reducing file size and forcing JPEG format) is deployed and saved on the server.
* The resources allocated to the function are upgraded to 512MB RAM to handle heavy image files.