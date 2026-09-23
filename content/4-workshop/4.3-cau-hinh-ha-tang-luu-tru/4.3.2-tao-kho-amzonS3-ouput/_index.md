---
title: "Create Amazon S3 Output Bucket (Thumbnail Repository)"
weight: 3
pre: " <b> 4.3.2 </b> "
---

## Detailed Instructions:
Similar to the Input bucket creation workflow, we will create a separate space to store the results returned by AWS Lambda. Separating the Output bucket helps prevent infinite loops—a classic error where Lambda saves new files back into the original bucket and continuously triggers itself.

**Step 1: Start Creating the Output Bucket**
1. Return to the Buckets list interface of the S3 service.
2. Click the **Create bucket** button again.

![alt text](/Workshop/images/4/image1.png)

**Step 2: Configure Output Bucket Information**
1. **AWS Region:** Select **US East (N. Virginia) us-east-1**.
2. **Bucket name:** Enter the exact name `kho-anh-nho-cua-toi-1`.

![alt text](/Workshop/images/4/image5.png)

**Step 3: Complete the Configuration**
1. Similar to the Input bucket, keep the **Block all public access** setting enabled. When the Web application needs to load thumbnails, the system will use Pre-signed URLs (URLs with signatures expiring after 300 seconds) to display images securely.
2. Scroll to the bottom, review the information, and click **Create bucket**.

![alt text](/Workshop/images/4/image3.png)
![alt text](/Workshop/images/4/image6.png)