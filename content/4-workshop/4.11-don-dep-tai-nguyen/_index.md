---
title: "Resource Clean-up"
weight: 11
pre: " <b> 4.11 </b> "
---

# RESOURCE CLEAN-UP (CLEAN-UP)

## Objectives
Remove all resources and services initialized on AWS during the practice session. Ensure the cloud environment is completely cleaned up to meet the Optimization criteria: Avoid incurring costs (Zero-cost) after the project ends.

## Overview
In a cloud computing environment, storage services (like S3, DynamoDB) will continue to charge based on storage capacity even if you are no longer running the application. Therefore, resource clean-up is a mandatory skill for every Cloud Engineer.

To ensure a smooth deletion process without being blocked by the system due to data constraints, we will proceed with deletion in a sequential rule: You must empty the data inside the storage buckets first before deleting the bucket itself, followed by deleting the compute server, database, activity logs, and finally cleaning up the security permission groups.

## Detailed Implementation Steps

### Step 1: Delete Amazon S3 Storage Buckets (Very Important)
*Note: AWS does not allow deleting an S3 bucket if it still contains any files inside. You must "Empty" it before you can "Delete" it.*
1. Access the S3 service, check the box to select the `kho-anh-goc-cua-toi-1` bucket.
2. Click the **Empty** button on the top menu, type `permanently delete` to confirm the deletion of all original images inside.

![alt text](/Workshop/images/4/4.11/image1.png)

3. Return to the list, select the `kho-anh-goc-cua-toi-1` bucket again, click the **Delete** button, and type the bucket name to confirm permanently deleting the bucket.

![alt text](/Workshop/images/4/4.11/image2.png)

4. Repeat the same Empty and Delete operations for the remaining 2 buckets: `kho-anh-nho-cua-toi-1` (Output Bucket) and `trang-web-xu-ly-anh-cua-toi` (Static Website Bucket).

![alt text](/Workshop/images/4/4.11/image3.png)

### Step 2: Delete Amazon DynamoDB Database Table
1. Access the DynamoDB service, select **Tables** on the left menu.
2. Check the box for the `ThongTinAnh` table.
3. Click the **Delete** button, type `confirm` to confirm the deletion of all historical metadata.

![alt text](/Workshop/images/4/4.11/image4.png)

### Step 3: Delete AWS Lambda Processing Function
1. Access the Lambda service, select the **Functions** tab.
2. Check the box for the `HamXuLyAnh12` function.
3. Click **Actions** $\rightarrow$ Select **Delete**, type `delete` to confirm deleting the Python source code.

![alt text](/Workshop/images/4/4.11/image5.png)
![alt text](/Workshop/images/4/4.11/image6.png)

### Step 4: Delete Amazon CloudWatch Logs
1. Access the CloudWatch service, find the **Logs** $\rightarrow$ **Log Management** section on the left menu.
2. Find and check the log group named `/aws/lambda/HamXuLyAnh12` (or equivalent).
3. Click **Actions** $\rightarrow$ **Delete log group** and confirm.

![alt text](/Workshop/images/4/4.11/image7.png)

### Step 5: Delete AWS IAM Security Identities
1. Access the IAM service, go to the **Roles** section.
2. Find the "Employee ID card" `RoleChoLambda`, check the box and click **Delete**.

![alt text](/Workshop/images/4/4.11/image8.png)

3. Switch to the **Users** section, select the IAM User account you created in Chapter 2, proceed to **Deactivate** the Access Key, delete the Key, and then delete this IAM User entirely.

![alt text](/Workshop/images/4/4.11/image9.png)

## Expected Outcomes
* All original images, compressed images, database history, and static web source code have been completely removed from the system.
* The AWS Learner Lab environment returns to its initial clean state.
* Ensure there will be no hidden storage or operational fees deducted in the future.