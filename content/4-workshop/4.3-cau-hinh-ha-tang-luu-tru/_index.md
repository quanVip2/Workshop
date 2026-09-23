---
title: "Configuring Storage Infrastructure (Creating Amazon S3 Input and Output Buckets)"
weight: 3
pre: " <b> 4.3 </b> "
---


## Objectives
Initialize two independent Object Storage buckets on the AWS cloud platform. Ensure proper configuration of the Region and Bucket Names so that the Frontend source code can smoothly upload images to the Input bucket and read thumbnails from the Output bucket.

## Overview
In the Serverless Automated Image Processing System architecture, Amazon S3 (Simple Storage Service) acts as the physical storage location for graphic files.

Instead of storing everything in one place, the system is designed with two separate buckets:

* **Input Bucket (Source Bucket):** Receives large original images uploaded by the user's browser. The appearance of a new file here acts as the trigger that activates the AWS Lambda function.
* **Output Bucket (Destination Bucket):** Stores only the ultra-lightweight compressed images produced by Lambda, used to return and display them on the Web interface (via Pre-signed URLs) to save bandwidth.

## Practice Content
This practice section includes two main procedures:

* Initialize the S3 Input bucket (`kho-anh-goc-cua-toi-1`) in the `us-east-1` region.
* Initialize the S3 Output bucket (`kho-anh-nho-cua-toi-1`) in the same `us-east-1` region.

## Expected Outcomes
* Two S3 buckets are successfully created on the system.
* The names of both buckets perfectly match the `INPUT_BUCKET` and `OUTPUT_BUCKET` constants declared in the `index.html` file.
* The buckets are deployed in the correct region, ready for integrating Event Notification workflows in subsequent chapters.