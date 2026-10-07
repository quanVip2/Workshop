---
title: "Deploying Microservices Cluster (Lambda Functions)"
weight: 7
pre: " <b> 4.7 </b> "
---

## Objectives
Setup and program the entire cluster of **4 AWS Lambda functions** operating as independent microservices. This function cluster handles all business logic of the system: from securely issuing Presigned URLs, automatically compressing images with AI Rekognition integration, to querying personalized history under multi-tenant security standards.

## Microservices Architecture Overview
Instead of stuffing all processing into a single function, the system is decoupled into 4 specialized functions:
* **4.7.1 `GenerateUploadUrl` Function:** Receives requests from API Gateway, creates temporary signatures for the frontend to upload directly and securely to the S3 Input bucket.
* **4.7.2 `HamXuLyAnh` Function:** Listens to S3 events, automatically compresses images using Pillow, calls **Amazon Rekognition** for AI analysis, and writes metadata to DynamoDB.
* **4.7.3 `GetUserHistory` Function:** Queries the DynamoDB table by user email, filters data, handles Decimal types, and returns the history list along with storage statistics.
* **4.7.4 `GenerateDownloadUrl` Function:** Issues temporary signatures for users to view/download finished images from the S3 Output bucket.

![Cluster of 4 Lambda Microservices in the System](/Workshop/images/4/4.7/2.1.png)