---
title: "Create Amazon S3 Input Bucket (Source Image Repository)"
weight: 1
pre: " <b> 4.3.1 </b> "
---



## Detailed Instructions:

**Step 1: Access the S3 Service**
1. In the top search bar of the AWS Management Console interface, type **S3** and select the S3 service.
2. Click the orange **Create bucket** button in the top right corner of the screen.

![alt text](/Workshop/images/4/image1.png)

**Step 2: Configure Input Bucket Information**
1. **AWS Region:** Ensure you select the correct **US East (N. Virginia) us-east-1**. This is crucial so that the S3 bucket resides in the same data center as the Lambda function, ensuring the fastest file transmission speed.
2. **Bucket name:** Enter the exact name `kho-anh-goc-cua-toi-1`.

![alt text](/Workshop/images/4/image2.png)

**Step 3: Configure Basic Access Permissions**
1. Scroll down to the **Object Ownership** section and keep the default as **ACLs disabled**.
2. Scroll down to the **Block Public Access settings for this bucket** section. Keep the checkmark in the **Block all public access** box.
3. Scroll to the bottom and click the **Create bucket** button.

![alt text](/Workshop/images/4/image3.png)
![alt text](/Workshop/images/4/image4.png)