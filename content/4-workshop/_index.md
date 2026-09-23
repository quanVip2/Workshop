---
title: "Workshop"
weight: 4
pre: " <b> 4. </b> "
---

## IMPLEMENTING AN AUTOMATED SERVERLESS IMAGE PROCESSING SYSTEM ON AWS

### Overview
In this workshop, we will build and deploy an Automated Image Processing System (Thumbnail Generator) using a Serverless Event-driven architecture on AWS.

The solution utilizes core AWS services such as Amazon S3 (for storing original images, output images, and hosting the static web interface), AWS Lambda (for graphic processing and image compression using Python 3.12 and Pillow Layer), Amazon DynamoDB (for storing metadata and processing history), and AWS IAM (for managing security access permissions) to build a platform capable of automatic scaling, zero server management, and cost optimization.

Throughout this workshop, you will prepare the AWS Learner Lab account environment, configure cloud storage repositories, set up a NoSQL database, program a serverless processing function integrated with external libraries (Layers), configure the event trigger flow between S3 and Lambda, deploy the user interface to static web hosting, test the entire application across multiple independent devices, and finally clean up all created AWS resources.

---

### Contents

1. [Workshop Overview](4.1-tong-quan-workshop/)
2. [Prerequisites](4.2-dieu-kien-chuan-bi/)
3. [Storage Infrastructure Configuration](4.3-cau-hinh-ha-tang-luu-tru/)
4. [NoSQL Database Setup](4.4-thiet-lap-co-so-du-lieu-nosl/)
5. [System Access Control](4.5-cap-quyen-truy-cap-he-thong/)
6. [Processing Logic Implementation](4.6-trien-khai-logic-xu-ly/)
7. [Event Flow Configuration](4.7-cau-hinh-luong-su-kien/)
8. [Domain and Web Hosting Configuration](4.8-cau-hinh-ten-mien/)
9. [System Monitoring](4.9-giam-sat-he-thong/)
10. [System Testing](4.10-kiem-thu-he-thong/)
11. [Resource Cleanup](4.11-don-dep-tai-nguyen/)