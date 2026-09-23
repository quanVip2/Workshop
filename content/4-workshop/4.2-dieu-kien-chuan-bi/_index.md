---
title: "Prerequisites"
weight: 2
pre: " <b> 4.2 </b> "
---

## Objectives
Ensure readers can access the AWS Management Console, set up an IAM account with appropriate security permissions to obtain Access Keys, and have the Web interface source code ready before starting to deploy core services.

## 1. Required Tools
Unlike traditional applications, this project applies a 100% Serverless architecture, so it does not require installing server software, Node.js, or Docker on your personal machine. All infrastructure configurations are performed directly on the AWS Management Console.

You only need to prepare:

* **AWS Account:** Has access to the AWS Management Console.
* **Web Browser:** Google Chrome, Coc Coc, or Microsoft Edge are recommended for running and testing the interface.
* **Code Editor:** Visual Studio Code (or Notepad++) used to edit parameters in the source code.
* **Project Source Code:** The `index.html` file containing the static Web interface framework and AWS SDK connection logic (available in the appendix).

## 2. Implementation Steps

**Step 1: Log in to the AWS Console and check the Region**
1. Log in to the AWS Management Console.
2. **Checkpoint:** Look at the top right corner of the screen to ensure the selected Region is **us-east-1 (N. Virginia)**. All storage and compute resources for this workshop will be centralized in this region to optimize speed and avoid cross-region errors.

**Step 2: Create access keys (IAM Access Key) for the Web application**
For the Web interface (running on the user's browser) to securely connect to the S3 bucket and DynamoDB database, we need to provide it with a set of identification keys.

1. From the AWS Console search bar, access the **IAM (Identity and Access Management)** service.
2. Navigate to the **Users** section and select the user you want to grant permissions to, which is `WebUser`.
3. Switch to the **Security credentials** tab.
4. Scroll down to the **Access keys** section and click the **Create access key** button.
5. Download the CSV file or carefully copy the 2 strings: `Access key ID` and `Secret access key`.
![Create Access Key](/Workshop/images/4/image2.png)

**Step 3: Integrate the security keys into the source code**
1. Open the `index.html` file using Visual Studio Code.
2. Locate the AWS SDK configuration code block (in the `<script>` section) and enter the 2 Key values obtained in Step 2 into the correct positions.
![Configuration](/Workshop/images/4/image3.png)
3. **Checkpoint:** Successfully save the `index.html` file. At this point, the source code is ready to connect to the cloud infrastructure.

## 3. Expected Outcomes
* Successfully log in to the AWS Management Console in the `us-east-1` region.
* Successfully create and securely store the identification access keys (Access Key ID & Secret Access Key) from the IAM service.
* The project source code (`index.html`) has been successfully updated with the security keys, ready for the resource deployment steps in the next chapter.