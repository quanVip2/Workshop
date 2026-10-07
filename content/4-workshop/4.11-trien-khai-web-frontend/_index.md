---
title: "Deploying Web Frontend & Statistics Dashboard"
weight: 11
pre: " <b> 4.11 </b> "
---

## Objectives
Integrate all backend services (Cognito, API Gateway) into the user interface (Frontend). Deploy the Analytics Dashboard system to display personal data statistics, AI labels, and finally publish the website to the public internet (Public URL).

## Interface Overview
Our Web Application is built as a **Single Page Application (SPA)** using vanilla HTML, CSS, and JavaScript, requiring no Node.js or Webpack installation. 

The interface is divided into two distinct, strictly protected states:
1. **Guest Mode:** Displays only the Sign In / Sign Up / OTP Verification form. The system connects with the `amazon-cognito-identity-js` library to interact with AWS.
2. **Authenticated Mode:** Displays the upload area, the capacity-saving statistics dashboard, and the processing history table containing AI labels from Amazon Rekognition.

## Practical Content
Frontend deployment will go through 3 core steps:
* **4.10.1 Authentication Configuration (Cognito UI):** Embed User Pool and Client ID parameters.
* **4.10.2 API & Dashboard Integration:** Embed the Invoke URL from API Gateway, display AI tags, and calculate percentage savings.
* **4.10.3 Deploy Website:** Deploy source code to the Netlify platform (or S3 Static Hosting) to get a live access link.

![alt text](/Workshop/images/4/4.11/2.1.png)
*Image Caption: Completed interface of the Enterprise Image Processing System.*