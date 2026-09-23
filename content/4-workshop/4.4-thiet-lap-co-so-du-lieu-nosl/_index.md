---
title: "NoSQL Database Setup"
weight: 3
pre: " <b> 4.3 </b> "
---

## Objectives
Initialize a non-relational database (NoSQL) table on AWS to store image processing history (Metadata) including: File name (with the user's anonymous code), file size after compression, and processing time. Ensure that anyone reading the document can independently recreate this data structure.

## Reasons for Service Selection (Architecture Design)
In a Serverless architecture, Amazon DynamoDB is chosen as an alternative to traditional relational databases (like MySQL/PostgreSQL on Amazon RDS) for 3 core reasons:

* **Fully Serverless:** No need to provision, manage, or maintain virtual servers.
* **Flexible (Schema-less):** Easy to add or remove data fields (such as Size, File type) in future updates without breaking the table structure.
* **Cost Optimization:** Charged per read/write request (Pay-per-request). When the application has no users, the database storage cost is virtually zero.

## Implementation Steps (End-to-End Deployment)

**Step 1: Access the DynamoDB Service**
1. In the AWS Management Console, use the top search bar, type **DynamoDB**, and select this database service.
2. Ensure the Region in the top right corner is still set to **us-east-1 (N. Virginia)**.

**Step 2: Initialize the Data Table (Create Table)**
1. On the DynamoDB Dashboard, click the orange **Create table** button.
2. The browser will navigate to the detailed configuration page; you need to accurately enter the following parameters (to match the prepared Frontend source code):
   * **Table name:** Enter `ThongTinAnh`
   * **Partition key:** Enter `TenHinhAnh`. Next to it, keep the data type as **String**. *(This is the Primary Key used to distinguish images and is a mandatory condition for the Web interface to execute the `deleteItem` command to delete images).*
   * **Sort key:** Leave blank.

![Image](/Workshop/images/4/4.3/image1.png)

**Step 3: Cost Optimization and Basic Security**
1. Scroll down to the **Table settings** section. Instead of leaving it as Default, select **Customize settings** to optimize costs for the project.
2. Under the **Read/write capacity settings** section:
   * Select **On-demand**. This setting helps the data table operate according to Serverless standards: charging only when read/write requests occur, solving the cost optimization problem for the system when idle.
3. Scroll to the bottom and click **Create table**.

![alt text](/Workshop/images/4/4.3/image2.png)

**Step 4: Initialization Status Testing (Metric/Log Checkpoint)**
The AWS system will take a few dozen seconds to provision resources.
1. Return to the **Tables** list screen.
2. Observe the **Status** column of the `ThongTinAnh` table. When the status changes from `Creating` to **Active** (green), the initialization process is complete.

## Expected Outcomes
* The NoSQL database table `ThongTinAnh` has been successfully initialized with an **Active** status.
* The Partition Key is correctly set to `TenHinhAnh`, fully compatible with the API on the Web interface.
* The system is configured in **On-Demand** mode, meeting the cost optimization standards for a real-world Serverless application.