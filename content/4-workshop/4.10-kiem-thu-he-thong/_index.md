---
title: "System Testing "
weight: 10
pre: " <b> 4.10 </b> "
---

## Objectives
Completely evaluate the end-to-end operation of the project. Verify the automation capabilities of the event flow (S3 Trigger Lambda) and, notably, test the multi-user data isolation feature through backend identification techniques.

## Overview
To solve the challenge of "each device having a different history" without building a complex registration/login system (such as Amazon Cognito), this project applies a clever trick on the Frontend: using LocalStorage.

When a browser accesses the website, it automatically generates a hidden identification code (e.g., `user_123xyz`). This code is automatically attached to the file name when uploaded to S3, passes through Lambda, and is stored in DynamoDB. When the interface fetches data back, it uses a filter to retrieve only the records belonging to that specific identification code, creating the illusion of completely independent and secure "personal spaces."

## Expected Outcomes
* The application uploads the original image to S3 and successfully retrieves the compressed image in about 8 seconds.
* Operation history across two different web browsers (e.g., Google Chrome and CoC CoC) is completely separate, preventing them from seeing each other's data.
* The download and delete history functions operate smoothly.

---

## Detailed Testing Steps

### Step 1: Experience on the First Device (e.g., Google Chrome)
1. Open the S3 Static Website link using the Google Chrome browser<http://trang-web-xu-ly-anh-cua-toi.s3-website-us-east-1.amazonaws.com/>

![alt text](/Workshop/images/4/4.10/image1.png)

2. Click on the image upload area, and select a large-sized image from your computer.

![alt text](/Workshop/images/4/4.10/image2.png)

3. Click **UPLOAD IMAGE TO SYSTEM**.

![alt text](/Workshop/images/4/4.10/image3.png)

4. Observe the status line: Changes from *"Uploading original image to S3 bucket..."* to *"Waiting for system to compress image (8s)..."* and finally *"Completed!"*.

![alt text](/Workshop/images/4/4.10/image4.png)

5. The thumbnail appears. Click **Open / Download this image** to check the quality and see how much the actual file size has been reduced compared to the original image.

![alt text](/Workshop/images/4/4.10/image5.png)

6. Scroll down to the Data History section; you will see the information of the recently uploaded image (the identification prefix has been stripped so the interface displays a clean original file name).

![alt text](/Workshop/images/4/4.10/image6.png)

> 📸 *Photo Guide 1: Take a full-screen screenshot of the Chrome browser showing the history table with 1-2 images you just tested.*

### Step 2: Verify Independent Space on the Second Device (e.g., CoC CoC)
1. Keep the web page open in Chrome, then open an additional CoC CoC browser (or open an Incognito Tab).
2. Paste the website link into CoC CoC.
3. Scroll down to the Data History section; you will see the message: *"You have not uploaded any images yet"*. Even though you just uploaded an image in Chrome, CoC CoC cannot see it thanks to the LocalStorage identification mechanism.

![alt text](/Workshop/images/4/4.10/image7.png)

4. Try uploading a different image (e.g., Image B) on CoC CoC. At this point, the history in CoC CoC shows Image B, while the history in Chrome (after clicking Refresh) still shows only Image A. 
   
![alt text](/Workshop/images/4/4.10/image8.png)

$$\rightarrow \text{The Multi-user feature works exceptionally well!}$$

> 📸 *Photo Guide 2: Take a screenshot of the CoC CoC browser displaying the "You have not uploaded any images yet" interface to prove the data isolation feature.*

### Step 3: Test the Delete Feature
1. Return to Chrome, and click the 🗑️ **Delete** button on an image in the history table.
2. A confirmation dialog will appear, select **OK**.

![alt text](/Workshop/images/4/4.10/image9.png)

3. The interface automatically reloads, and the image disappears from the history (DynamoDB's `deleteItem` command has been executed).

![alt text](/Workshop/images/4/4.10/image10.png)

# AWS SERVICES USED

During the application testing process, the platform integrated the following AWS services:

| AWS Service | Purpose |
| :--- | :--- |
| **Amazon S3** | Storing static web interface, original images, and compressed images |
| **AWS Lambda** | Providing a serverless compute environment to automatically process and compress images |
| **Amazon DynamoDB** | Storing user operation history data (metadata) |
| **AWS IAM** | Providing secure access permissions for Frontend source code and internal services |
| **Amazon CloudWatch** | Monitoring application health, recording errors, and system logs |

The successful operation of all interfaces proves that the Automated Image Processing System application has been fully deployed and operates stably on the AWS cloud computing infrastructure.