---
title: "Assign Permissions for Lambda"
weight: 2
pre: " <b> 4.5.2 </b> "
---

**Step 1: Select the Policies**
In the **Add permissions** step, AWS provides thousands of different policies. Use the search bar to find and check (☑) the boxes next to exactly the following 3 Policies:

*   Type `AmazonS3FullAccess` ➔ Check the box.
    *(Purpose: Allows Lambda to retrieve images from the S3 Input and save the compressed images to the S3 Output).*
    ![alt text](/Workshop/images/4/4.4/image4.png)
*   Clear the search bar, then type `AmazonDynamoDBFullAccess` ➔ Check the box.
    *(Purpose: Allows Lambda to write history logs - Metadata into the NoSQL data table).*
    ![alt text](/Workshop/images/4/4.4/image5.png)
*   Clear the search bar, then type `AWSLambdaBasicExecutionRole` ➔ Check the box.
    *(Purpose: This is the core Policy meeting the project's Testing and Monitoring requirements, granting Lambda the permission to create Log Groups and write activity/error logs to Amazon CloudWatch).*
    ![alt text](/Workshop/images/4/4.4/image6.png)

After checking all 3 items, click the **Next** button.

**Step 2: Name and Complete**
At the **Name, review, and create** step:

*   **Role name:** Enter a meaningful name, for example: `RoleChoLambda`.
*   **Description:** You can add a note: *Grant S3, DynamoDB, and CloudWatch permissions for the Thumbnail Generator image compression function.*

Scroll down to the **Permissions boundary** section and double-check the policy list to ensure that all 3 Policies (`AmazonS3FullAccess`, `AmazonDynamoDBFullAccess`, `AWSLambdaBasicExecutionRole`) are present.

Click the **Create role** button at the bottom to finish.
![alt text](/Workshop/images/4/4.4/image7.png)