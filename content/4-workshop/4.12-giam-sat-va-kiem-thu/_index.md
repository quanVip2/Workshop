---
title: "System Testing and Monitoring (CloudWatch)"
weight: 12
pre: " <b> 4.12 </b> "
---

## Objectives
Comprehensively evaluate the end-to-end operational workflow of the project. Verify multi-tenant security authentication capabilities (Amazon Cognito), the automated image processing workflow integrated with Artificial Intelligence (Amazon Rekognition), and system monitoring and error tracing capabilities via Amazon CloudWatch.

## Overview
Unlike testing applications that use LocalStorage to create virtual identities, this Enterprise system is strictly secured by Amazon Cognito and API Gateway. 

Every accessing user must have an authenticated Email account. The system uses JWT Tokens for authorization and routing. Whenever the browser requests to upload an image or retrieve history, this token is decoded by API Gateway to cross-reference with the DynamoDB database table, creating an entirely independent, secure, and personalized workspace for each user. All background processing procedures are logged by AWS on CloudWatch for easy tracking by administrators.

## Expected Results
* Registration, OTP code submission, and Email Sign-In interfaces operate smoothly.
* Images upload successfully, and the statistics dashboard accurately calculates optimized size percentages.
* The AI service automatically extracts labels (Tags) matching the image content.
* Data from Account A does not cross-display into Account B (Multi-tenant Isolation).
* Administrators can view detailed Lambda execution times on CloudWatch Logs.

---

## Detailed Testing Steps

### Step 1: Experiencing Authentication and AI Features on Account A
1. Open the deployed [website](https://trang-web-xu-ly-anh-cua-toi.s3.us-east-1.amazonaws.com/index.html) link on S3 using a web browser.
2. At the **System Security** interface, click on "Don't have an account? Sign up". Enter a real Email and a Password (containing uppercase letters, lowercase letters, numbers, and special characters).
3. Check your Inbox (Email) for the 6-digit OTP code sent by Amazon Web Services, and enter it into the web to authenticate.
4. Upon successful login, upload a large-sized image to the system.
5. Observe the processing status. After a few seconds, the system returns a "Complete" notification.
6. **Check the Dashboard & History Table:**
   * The dashboard will automatically update: Total Images (1), Total Original Size (e.g., 2MB), Compressed Size (e.g., 150KB), and display Saved Percentage (e.g., 92%).
   * The **AI Tags 🤖** column in the history table will display English keywords (e.g., *Person, Face, Electronics*) accurately reflecting the image content.

![alt text](/Workshop/images/4/4.12/2.1.png)
*Image Caption: Personal interface of Account A after image processing.*

### Step 2: Verifying Multi-tenant Data Isolation
1. Keeping the Account A tab open, open an additional **Incognito Window** tab or use another browser (e.g., open Cốc Cốc while using Chrome).
2. Access the website, perform Registration and Sign-In with a **completely different Email** address (Account B).
3. Upon successful login, you will see Account B's Dashboard displaying **0**, and the history notification: *"You have not uploaded any images yet"*.
4. Account A's data is completely isolated and absolutely protected thanks to Cognito's JWT Token mechanism and API Gateway routing.

![alt text](/Workshop/images/4/4.12/2.2.png)
*Image Caption: Secure data isolation capability between accounts.*

### Step 3: Monitoring the System with Amazon CloudWatch
A Serverless system has no servers for you to access to view logs directly, so AWS provides CloudWatch to collect all execution traces.

1. Log in to the AWS Management Console, search for and select the **CloudWatch** service.
2. In the left-hand menu, under *Logs*, select **Log groups**.
3. Find and click on the log group of the image processing function: `/aws/lambda/HamXuLyAnh`.
4. Click on the topmost recent log stream record.
5. Here, you will see system notifications printed out (e.g., *Image compression and AI analysis successful!*), accompanied by **Billed Duration** parameters (execution time measured in milliseconds) and **Memory Used** (the actual RAM amount used by the function for graphics processing).

![alt text](/Workshop/images/4/4.12/2.3.png)
*Image Caption: Monitoring Lambda function execution via CloudWatch Logs.*

---

## SUMMARY OF AWS SERVICES USED

Throughout the construction of this Enterprise architecture, the system has applied a powerful ecosystem consisting of the following AWS cloud services:

| AWS Service | Role in the System |
| :--- | :--- |
| **Amazon Cognito** | Manages identities, sign-up, sign-in, and issues secure JWT Tokens. |
| **Amazon API Gateway** | Central REST API gateway, validates tokens, and protects Lambda from unauthorized access. |
| **AWS Lambda** | Microservices cluster responsible for URL authorization, graphics processing, and history queries. |
| **Amazon Rekognition** | Applies Artificial Intelligence (Machine Learning) to recognize subjects and assign image tags. |
| **Amazon S3** | Secure object storage for original images (Input) and thumbnails (Output). |
| **Amazon DynamoDB** | NoSQL database storing all metadata trails, serving statistics dashboard queries. |
| **AWS IAM** | Grants minimal security permissions (Least Privilege) among cloud services. |
| **Amazon CloudWatch**| Collects system logs (Logs), monitors errors, and measures performance automatically. |

The fact that the entire system operates stably and accurately proves that you have successfully deployed a complete serverless web architecture meeting the security and performance standards of a genuine Enterprise system.