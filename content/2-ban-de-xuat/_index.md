---
title: "Proposal"
weight: 2
pre: " <b> 2. </b> "
---

# ENTERPRISE SERVERLESS IMAGE PROCESSOR: AN AI-INTEGRATED SERVERLESS IMAGE PROCESSING SYSTEM

## 1. General Information

* **Project Title:** Building an automated serverless image processing system integrated with AI and identity security on AWS.
* **Author:** Nguyễn Hồng Quân
* **Context:** In modern web applications and SaaS platforms, digital asset management (images) demands strict performance regarding loading speed, user data security, and intelligent analytics. This project builds a complete End-to-End solution applying an event-driven model, secure user authentication, and Artificial Intelligence (AI) analytics entirely on the AWS cloud platform.

## 2. Problem Statement & Objectives

### 2.1. Context & Problem
* **What does the system do?** The system provides a personalized image management platform. Authenticated users can securely upload images. The system automatically compresses them, converts formats (to JPEG), extracts keywords using AI (Rekognition), stores separate data histories for each account, and provides a space-saving statistics dashboard.
* **Target Users:** E-commerce platforms, content management systems (CMS), or SaaS applications requiring an absolutely secure multi-tenant image processing workflow.
* **Problem Solved:** Eliminates traditional server maintenance costs, resolves data leakage issues through temporary access grants (Presigned URLs), and automates image classification via AI instead of manual tagging.

### 2.2. Specific Objectives
* **Expected Output:**
  * User authentication and API protection via JWT Tokens.
  * A cluster of 4 AWS Lambda functions serving independent microservices roles.
  * AI application to automatically label image content.
  * A dashboard tracking history and individual capacity optimization efficiency.
* **Success Criteria:**
  * Authentication, authorization, image compression, and AI analysis occur fully automatically in under 5 seconds.
  * 100% of S3 storage is locked down (Block Public Access); users can only upload/view images via valid security signatures.
  * Each account's information can only be accessed and displayed by that specific account.

## 3. Architecture & Technical Design

### Architecture Diagram
![Serverless Image Processing System Architecture Diagram](/Workshop/images/so_do.png)

### 3.1. AWS Services Selection
* **Amazon Cognito:** Manages identities, sign-up/sign-in, and issues secure JWT Tokens.
* **Amazon API Gateway:** Central REST API gateway combined with a JWT Authorizer to block unauthorized access.
* **AWS Lambda:** Acts as the processing core with 4 independent functions: Upload Authorization (`GenerateUploadUrl`), Download Authorization (`GenerateDownloadUrl`), History Query (`GetUserHistory`), and Automated Image Processing (`HamXuLyAnh`).
* **Amazon Rekognition (AI):** Machine learning service that automatically performs visual analysis and extracts tags from uploaded images.
* **Amazon S3 (Simple Storage Service):** Stores Frontend (Static Web Hosting), Input Bucket (Original images), and Output Bucket (Compressed JPEG images).
* **Amazon DynamoDB:** High-performance NoSQL database storing metadata, owner email, compressed size, and AI keywords.
* **Amazon CloudWatch:** Monitors, collects logs, and measures overall system performance.

### 3.2. Security & Least Privilege
* **Frontend-Backend Security:** No static Access Keys in source code. All file access workflows utilize **Presigned URLs** (5-minute expiration).
* **IAM Permission Management:** Separated roles for each Lambda function complying with the Least Privilege principle (e.g., `GenerateUploadUrl` only has S3 PutObject permissions, with no delete or DB read privileges).

## 4. Potential Risks & Mitigation

* **Risk 1: Direct Access Data Breach to S3 Storage**
  * *Mitigation:* Configure global S3 Block Public Access. All upload/download actions must pass through the API Gateway + Lambda cluster to request temporary signatures (Presigned URLs) based on Cognito Tokens.
* **Risk 2: Format Errors and Special Characters During Upload**
  * *Mitigation:* The upload link-generating Lambda automatically strips original names containing sensitive characters, replacing them with a UUID combined with the Email (e.g., `user---upload_id.jpg`) to identify users and prevent HTTP 403 Signature errors.
* **Risk 3: Infinite Loop Event Trigger**
  * *Mitigation:* Separate into 2 Buckets (a dedicated Input Bucket and Output Bucket). Ensure the `HamXuLyAnh` function is only triggered by the Input bucket and writes results to the Output bucket.

## 5. Implementation Lab Steps

The project is deployed through standardized end-to-end steps:
* **Step 1:** Initialize an Amazon Cognito User Pool for account management.
* **Step 2:** Build Amazon S3 storage (Input, Output, Static Web) and DynamoDB tables.
* **Step 3:** Configure detailed IAM Policies & Roles for services.
* **Step 4:** Program the 4 AWS Lambda processing logic functions (Python) combining the Pillow library (graphics processing) and Boto3.
* **Step 5:** Build Amazon API Gateway, integrate Cognito Authorizer, and configure secure CORS.
* **Step 6:** Integrate Amazon Rekognition AI into the automated image processing pipeline (S3 Trigger).
* **Step 7:** Integrate Frontend source code (HTML/JS) to call APIs, test multi-tenant stream segmentation, and analytics dashboards.

## 6. Personal Contributions & Innovations

Unlike basic labs, this project has been upgraded with highly innovative features:
* **Artificial Intelligence (AI) Integration:** Automatically recognizes image subjects and assigns smart tags using Machine Learning (Amazon Rekognition).
* **Multi-tenant Architecture:** The system can identify owner emails, maintain isolated history storage, and secure personal privacy for individuals.
* **Analytics Dashboard:** The frontend automatically calculates total images, original size, compressed size, and the percentage of bandwidth/storage saved through the cloud.
* **Presigned Security Workflow:** Completely conceals the internal S3 storage architecture from the public internet, establishing an enterprise-grade security standard.