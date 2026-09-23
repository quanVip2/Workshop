---
title: "Workshop Overview"
weight: 1
pre: " <b> 4.1 </b> "
---

## Objectives
This workshop guides you through deploying an Automated Image Processing System (Thumbnail Generator) application on the AWS platform using a serverless architecture, managed services, and an event-driven architecture. Upon completing the workshop, you will be able to deploy a complete graphic-processing web application with auto-scaling capabilities, cost optimization (zero-cost when idle), and independent workspace management for multiple users.

## 1. Introduction to the Problem and Solution
The Automated Image Processing System is a web application that simulates the background job workflow of large platforms (like Facebook, Shopee), where users upload original images and the system automatically generates a thumbnail version to optimize page load speed. The system supports features such as image uploading, automatic size compression (using the Pillow library), processing history management, downloading/viewing compressed images, and allocating independent data spaces for each device.

Instead of deploying the application on a traditional server (EC2) running 24/7 causing resource waste, this workshop applies a Serverless architecture on AWS. The static interface of the application is stored and distributed by Amazon S3 (Static Website Hosting). Original and thumbnail images are also safely stored in independent Amazon S3 buckets.

The image compression process is executed by an AWS Lambda function (Python 3.12) integrated with a Lambda Layer (Klayers) to load the Pillow graphic library, ensuring powerful computing capability without server management. All processing history data (Metadata) is automatically recorded into the Amazon DynamoDB NoSQL database. The system is monitored via Amazon CloudWatch and strictly manages access permissions using AWS IAM.

## 2. System Architecture
The system architecture includes the following main components:

* Users (Client Browser)
* Static Web Hosting (Interface presentation)
* Object Storage Services (Input & Output)
* Serverless Compute Service
* NoSQL Database (History logging)
* Identity and Access Management
* System Monitoring

![Figure 1 – Automated Image Processing System Architecture](/images/architecture-diagram.png)
*Figure 1 – Automated Image Processing System Architecture (Note: Ensure you have saved the architecture diagram image in the `/images/architecture-diagram.png` folder)*

## 3. System Workflow
The main processing flow of the system occurs in the following steps:

1. Users access the website via the URL provided by the S3 Static Website Hosting feature.
2. The web browser generates a hidden identifier (Device ID) using LocalStorage, automatically attaches this ID as a prefix to the image, and uploads it directly to the Amazon S3 repository (Input Bucket) via the AWS SDK.
3. The `s3:ObjectCreated` event from the Input Bucket immediately triggers the AWS Lambda function.
4. The AWS Lambda function (provisioned with 512MB RAM and a 15s Timeout) loads the original image into memory, uses the Pillow library (from the Lambda Layer) to reduce resolution, compresses quality to 50%, and converts it to JPEG format.
5. AWS Lambda pushes the ultra-lightweight compressed image to the Amazon S3 repository (Output Bucket).
6. Simultaneously, AWS Lambda logs the information (File name, new size, processing time) into the Amazon DynamoDB database.
7. The user's web browser continuously listens and retrieves the thumbnail from the S3 Output (via Pre-signed URL) to display.
8. The browser calls the Amazon DynamoDB query API, applying filter logic to only fetch and display the image processing history belonging to that specific user's device.
9. Activity logs and Lambda function execution errors (if any) are sent to Amazon CloudWatch for monitoring and troubleshooting.

## 4. Services Used
The workshop utilizes the following AWS services:

* **Compute Services**
  * AWS Lambda
  * AWS Lambda Layers
* **Storage Services**
  * Amazon S3 (Object Storage & Static Website)
  * Amazon DynamoDB (NoSQL Database)
* **Security & Management**
  * AWS Identity and Access Management (IAM)
* **Monitoring**
  * Amazon CloudWatch

## 5. Expected Outcomes
After completing the workshop, you will be able to:

* Program and configure a static web interface that communicates directly with AWS without a backend server (via AWS SDK for JavaScript).
* Deploy an image storage solution and Static Website Hosting on Amazon S3.
* Design a non-relational database (NoSQL) table with Amazon DynamoDB to record Logs/Metadata.
* Integrate third-party libraries (C-compiled modules like Pillow) into the AWS Lambda environment via the Lambda Layers feature.
* Build an event-driven automation flow: using S3 file upload events to trigger Lambda.
* Configure compute power (Memory, Timeout) for Lambda to handle heavy graphic tasks.
* Analyze system errors and monitor architecture operations through Amazon CloudWatch Logs.
* Delete all AWS resources after completing the workshop to avoid incurring costs.