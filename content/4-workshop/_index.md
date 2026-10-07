---
title: "Workshop"
weight: 4
pre: " <b> 4. </b> "
---

## DEPLOYING AN AI-INTEGRATED SERVERLESS IMAGE PROCESSING SYSTEM ON AWS

### Overview
In this workshop, we will build and deploy an Enterprise-grade Automated Serverless Image Processor. The system utilizes a multi-tenant architecture, identity security, and Artificial Intelligence (AI) integration entirely on the AWS platform.

The solution leverages core AWS services including: 
* **Amazon Cognito:** Manages authentication and issues secure token flows (JWT).
* **Amazon API Gateway:** Builds a secure REST API gateway using Presigned URL techniques to avoid exposing security configurations to the frontend.
* **AWS Lambda:** Deploys a microservices cluster consisting of 4 independent business logic functions using Python 3.12 (Authorization, Image Compression, History Query).
* **Amazon Rekognition:** Applies Machine Learning to automatically analyze and assign AI tags to images.
* **Amazon S3 & DynamoDB:** Stores static files, metadata, and space-saving statistics per individual account.
* **AWS IAM:** Manages access permissions under strict adherence to the Least Privilege principle.

Throughout this workshop, you will be guided step-by-step through configuring the security environment, setting up storage repositories, programming AI-integrated serverless function clusters, configuring event-driven flows, deploying a frontend web interface with an integrated Personal Statistics Dashboard, testing independent account stream isolation, and finally cleaning up resources to optimize costs.

---

### Contents

1. [Workshop Overview](4.1-tong-quan-workshop/)

2. [Prerequisites](4.2-dieu-kien-chuan-bi/)

3. [Configuring Identity Authentication with Amazon Cognito](4.3-cau-hinh-xac-thuc-cognito/) *(Newly added)*

4. [Configuring S3 Storage Infrastructure](4.4-cau-hinh-ha-tang-luu-tru/)

5. [Setting Up DynamoDB NoSQL Database](4.5-thiet-lap-co-so-du-lieu-nosql/)

6. [System Access Control (IAM)](4.6-cap-quyen-truy-cap-he-thong/)

7. [Deploying Microservices Cluster (Lambda) & AI Rekognition](4.7-trien-khai-logic-xu-ly/) *(Content updated)*

8. [Building REST API Gateway with Amazon API Gateway](4.8-xay-dung-cong-api-gateway/) *(Newly added)*

9. [Configuring Automated Event Flows (S3 Trigger)](4.10-cau-hinh-luong-su-kien/)

10. [Deploying Web Frontend & Statistics Dashboard](4.11-trien-khai-web-frontend/) *(Content updated)*

11. [System Testing and Monitoring (CloudWatch)](4.12-giam-sat-va-kiem-thu/)

12. [Resource Cleanup](4.13-don-dep-tai-nguyen/)