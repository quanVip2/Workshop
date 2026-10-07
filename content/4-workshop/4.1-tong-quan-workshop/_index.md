---
title: "Workshop Overview"
weight: 1
pre: " <b> 4.1 </b> "
---

## Objectives
This workshop guides you through deploying the **Enterprise Serverless Image Processor** application integrated with AI on the AWS cloud platform. 

By combining serverless architecture, managed services, Machine Learning analytics, and an event-driven architecture, this workshop helps you build a complete end-to-end solution. Upon completion, you will possess a web system capable of auto-scaling, cost optimization, intelligent image recognition using Artificial Intelligence, and enterprise-grade multi-tenant identity security.

## 1. Problem Introduction and Solution
In modern software systems (such as CMS and E-commerce), managing and optimizing digital assets is a mandatory requirement. However, manually building servers (EC2) to process images not only wastes resources during idle times but also introduces data security risks.

This workshop solves this problem by comprehensively applying the AWS Serverless ecosystem. The user interface is hosted on static Amazon S3 or Netlify. Identity data is strictly managed by **Amazon Cognito**, combined with **Amazon API Gateway** to form a robust API protection shield.

At the heart of the system is a cluster of 4 microservices functions running on **AWS Lambda** (Python 3.12). When an image upload event occurs, Lambda uses the Pillow graphics library to standardize images into lightweight JPEGs while calling the **Amazon Rekognition** service to use AI for extracting content labels (AI Tags). All data, including metrics measuring original and compressed sizes, is stored in the **Amazon DynamoDB** NoSQL database to output an analytics dashboard measuring efficiency for each individual user.

## 2. System Architecture
The system architecture consists of the following main component layers:

* **Presentation Layer:** Web Frontend interface.
* **Security & Authentication Layer:** User management, token issuance, and API access control.
* **API Layer:** REST API gateway routing requests.
* **Serverless Compute Layer:** A cluster of 4 Lambda functions (Upload, Download, History, Image Processing).
* **AI Layer:** Image analysis using Machine Learning.
* **Storage & Database Layer:** Static file and metadata storage.
* **Monitoring Layer:** Log and performance management.

![Figure 1 – AI-Integrated Automated Image Processing System Architecture](/Workshop/images/so_do.png)
*(Note: The image used is the V2 architecture diagram so_do.png you just created)*

## 3. System Workflow
The main processing workflow of the system takes place in 10 closed and secure steps:

1. The user accesses the website through the static frontend.
2. The user registers/logs in via **Amazon Cognito**. If successful, Cognito issues a valid **JWT Token**.
3. The browser sends a request attached with the JWT Token to **Amazon API Gateway**. API Gateway validates the token before allowing it to proceed.
4. The system calls the `GenerateUploadUrl` Lambda function to request authorization. Lambda returns a security signature (**Presigned URL**). The browser uses this URL to upload the image directly to the S3 Input Bucket.
5. The `s3:ObjectCreated` event from the Input Bucket immediately triggers the core `HamXuLyAnh` Lambda function.
6. The graphics processing Lambda function automatically changes the format of all image types to the `.jpg` standard, shrinks them, and compresses their size.
7. The Lambda function sends the compressed image through **Amazon Rekognition** for AI analysis and keyword (tag) extraction.
8. Lambda saves the finished image to the S3 Output Bucket; simultaneously writing all information (Owner Email, Original Size, Compressed Size, AI Tags) to **Amazon DynamoDB**.
9. The user's browser calls the `GetUserHistory` Lambda function through API Gateway to retrieve data. This function only queries DynamoDB for records matching the current user's email, calculates space-saving percentages, and renders them to the dashboard statistics table.
10. When the user clicks "View", API Gateway continues to call the `GenerateDownloadUrl` Lambda function to issue a temporary Presigned URL, helping the user download/view the image from S3 Output with absolute security.

**[IMAGE REQUEST 1: Screenshot of the Web Interface upon successful login displaying the Upload section and the Statistics Dashboard below (with displayed metrics and AI labels).]**
*Image Caption: User interface featuring upload capabilities, AI recognition, and analytics dashboard.*

## 4. AWS Services Used
The workshop utilizes a comprehensive AWS Serverless ecosystem, including:

* **Compute & Machine Learning**
  * AWS Lambda
  * Amazon Rekognition
* **Security & Network**
  * Amazon Cognito (User Pools)
  * Amazon API Gateway
  * AWS Identity and Access Management (IAM)
* **Storage & Database**
  * Amazon S3 (Object Storage & Block Public Access)
  * Amazon DynamoDB (NoSQL Database)
* **Monitoring**
  * Amazon CloudWatch

## 5. Achieved Results
Upon completing the workshop, you will master advanced cloud skills:

* Integrate secure user authentication systems with Amazon Cognito User Pools and manage login sessions via the JWT standard.
* Protect REST APIs using the Amazon API Gateway Authorizer mechanism, completely preventing unauthorized access.
* Build secure data communication workflows using "temporary signature" techniques (Presigned URLs), eliminating the risk of static Access Key leakage.
* Deploy a microservices architecture using AWS Lambda to decouple tasks: Upload authorization, download authorization, history retrieval, and background processing.
* Apply an event-driven architecture model to trigger automated image compression processes as soon as a new file arrives.
* Integrate Machine Learning services (Amazon Rekognition) into the processing system to automatically assign labels to images using AI.
* Design a multi-tenant NoSQL database with Amazon DynamoDB, serving the creation of an intuitive Analytics Dashboard.
* Clean up and manage AWS resources according to best practices to optimize costs.

![Image of created Lambdas (excluding NoteHandler which is yours)](/Workshop/images/4/4.1/2.1.png)