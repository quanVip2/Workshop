---
title: "Prerequisites"
weight: 2
pre: " <b> 4.2 </b> "
---

## Objectives
Ensure you have proper access to the AWS Management Console, set up the correct deployment region, and prepare your local code editing environment before building core services.

## 1. Required Tools
This project applies a 100% Serverless architecture combined with a static frontend, so you are not required to install virtual server software, Node.js, or Docker on your personal computer. All backend infrastructure configurations are performed directly on the AWS Management Console.

You only need to prepare:

* **AWS Account:** With access to the AWS Management Console (using an AWS Learner Lab account or personal account).
* **Web Browser:** Recommended to use Google Chrome, Cốc Cốc, or Microsoft Edge to run and test the API communication interface.
* **Code Editor:** Visual Studio Code (or Sublime Text, Notepad++) used to program the HTML/JS interface and configure Python functions.
* **Local Environment:** An empty folder on your computer to hold the project's frontend source code.

## 2. Implementation Steps

**Step 1: Log in to the AWS Console and Check the Region**
1. Log in to the AWS Management Console with your account.
2. **Checkpoint:** Observe the top right corner of the screen, ensuring the selected region is **US East (N. Virginia) `us-east-1`**. 
*Reason:* Consolidating all storage resources (S3), compute (Lambda), authentication (Cognito), and AI (Rekognition) in a single region optimizes connection speed, avoids latency, and completely eliminates cross-region service conflict errors.
![Displayed Region](/Workshop/images/4/4.2/2.1.png)

**Step 2: Prepare the Workspace**
1. Create a new folder on your computer named `Enterprise_Image_Processor`.
2. Open this folder using Visual Studio Code.
3. Create an empty file named `index.html`. This file will serve as the place where we program the entire web interface, Cognito login form, and dashboard in subsequent steps.

![Visual Code Screen](/Workshop/images/4/4.2/2.2.png)

---

### ⚠️ Critical Security Note (Security Paradigm Shift)
If you have previously worked on basic labs, you were often instructed to create an *IAM Access Key* and hardcode it directly into the HTML/JS source code to connect with the AWS SDK. **THIS IS A SEVERE SECURITY VULNERABILITY** in a real-world environment, as anyone inspecting the webpage source code (F12) can steal the key and take control of your AWS account.

In this Enterprise-grade workshop, we **ABSOLUTELY DO NOT** use static access keys on the frontend. 
Instead, our system utilizes a multi-layered security architecture:
* Users log in via **Amazon Cognito** to obtain a **JWT Token** (valid for only 1 hour).
* This token is sent to **Amazon API Gateway** for authentication.
* Once validated, the backend AWS Lambda issues a **Presigned URL** (a temporary signed link active for 5 minutes) so the web browser can safely upload/download images to/from S3 without knowing any system passwords.

---

## 3. Expected Results
* You have successfully logged into the AWS Management Console in the `us-east-1` region.
* You have successfully initialized the project folder and `index.html` file on your personal computer.
* You grasp the new security mindset: Do not use and do not embed IAM Access Keys into the frontend interface.