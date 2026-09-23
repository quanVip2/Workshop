---
title: "Project Proposal"
weight: 2
pre: " <b> 2. </b> "
---

# SERVERLESS IMAGE THUMBNAIL GENERATION SYSTEM

## 1. General Information

* **Project Title:** Serverless Image Thumbnail Generation System on AWS.
* **Author:** Đoàn Vũ Ngọc Ánh
* **Context:** In modern web applications, optimizing uploaded images is mandatory to reduce bandwidth and enhance user experience. This project builds a fully automated solution utilizing an event-driven model on the AWS cloud platform.

## 2. Problem Statement & Objectives

### 2.1. Context & Problem
* **What does the system do?** The system automatically detects image files when uploaded by users, generates thumbnails, stores them, and logs metadata into a database.
* **Target Users:** System administrators, web application developers for e-commerce or personal blogs.
* **Problem Solved:** Overcomes the high cost of traditional server resources (EC2 running 24/7), eliminates delays caused by manual processing, and optimizes operational costs through Serverless architecture.

### 2.2. Specific Objectives
* **Expected Output:**
  * Two separate image storage partitions (Input Bucket and Output Bucket).
  * An automated processing function triggered via S3 Event.
  * A table storing dimension and processing time information on a NoSQL database.
  * A real-time activity monitoring log system.
* **Success Criteria:**
  * Uploading an image to the source bucket results in the thumbnail appearing automatically in the destination bucket within 3 seconds.
  * Image information is fully recorded in the database without manual intervention.

## 3. Architecture & Technical Design

## Architecture Diagram
![Sơ đồ kiến trúc Hệ thống Tự động xử lý hình ảnh Serverless](/images/sodo.jpg)

### 3.1. AWS Services Selection
* **Amazon S3 (Simple Storage Service):** Used for file storage (divided into Input Bucket and Output Bucket) with high durability, low cost, and event notification support.
* **AWS Lambda:** Serverless compute service. Chosen because it requires no hardware management, charges only for actual request counts, and scales automatically based on load.
* **Amazon DynamoDB:** High-performance NoSQL database managing all lightweight structured data of image files.
* **Amazon CloudWatch:** Monitors, collects logs, and measures the performance of the Lambda function.

### 3.2. Security & IAM
* Configures a dedicated IAM Role for AWS Lambda.
* Strictly adheres to the Least Privilege principle: The Lambda function only has `GetObject` permission on the source bucket, `PutObject` on the destination bucket, logging permissions to CloudWatch, and write permissions to the designated DynamoDB table. Global administrator access (`AdministratorAccess`) is not used.

## 4. Potential Risks & Mitigation

* **Risk 1: Infinite Loop Event Trigger**
  * *Description:* If the Lambda function writes the result file back to the Input Bucket (where the event is triggered), it creates an infinite event loop, leading to resource exhaustion and heavy costs.
  * *Mitigation:* Design an architecture with two completely separated buckets (separate Input Bucket and Output Bucket). Ensure the Lambda function only listens to events from the Input Bucket and writes result files to the Output Bucket with a distinct prefix (`resized_`).
* **Risk 2: IAM Permission Denied**
  * *Description:* The Lambda function lacks read/write permissions for the bucket or cannot connect to the DynamoDB table due to misconfigured IAM Roles.
  * *Mitigation:* Carefully check the resource ARN configurations in the IAM Policy and use Amazon CloudWatch Logs to trace exact error codes upon execution failures.
* **Risk 3: Cost Overruns**
  * *Description:* Forgetting to clean up resources after testing leads to costs exceeding the Free Tier limits.
  * *Mitigation:* Establish predefined clean-up steps after completing labs and regularly check the AWS Billing console.

## 5. Implementation Lab Steps

The project is implemented through standardized end-to-end steps:
* **Step 1:** Initialize two Amazon S3 Buckets (Input and Output).
* **Step 2:** Create an Amazon DynamoDB table to log image metadata.
* **Step 3:** Establish an IAM Policy and IAM Role adhering to the Least Privilege principle.
* **Step 4:** Build an AWS Lambda function (Python) to handle copy and data writing logic.
* **Step 5:** Configure S3 Event Triggers to automatically activate the Lambda function upon new file arrivals.
* **Step 6:** Test and validate results on DynamoDB and check CloudWatch Logs.
* **Step 7:** Perform resource clean-up to optimize costs.

## 6. Personal Contributions & Customization

* **Custom Extensions:** Beyond simple file copying, the system integrates Amazon DynamoDB to automatically extract, shape, and store detailed information (file name, size, processing time) to support reporting and analytics.
* **Future Development Direction:** Integrate a static web frontend on S3 combined with CORS policies so end-users can interact directly through a web browser intuitively.