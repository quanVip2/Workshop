---
title: "Identity Authentication Configuration (Amazon Cognito)"
weight: 3
pre: " <b> 4.3 </b> "
---

## Objectives
Initialize and configure the Amazon Cognito service using the quick setup interface (Setup resources for your application). This is the step to establish a security layer to manage user accounts and issue the JWT Token standard for the entire system.

## Overview
In the Enterprise image processing system architecture, instead of storing passwords manually or allowing anonymous users to upload images freely, we use **Amazon Cognito**. 

The new AWS Cognito interface allows us to configure core components simultaneously:
* **User Directory:** Stores identity information and authenticates users via Email.
* **Application Integration:** Integrates directly with the Web application via App Client (supporting authentication through SDKs like `amazon-cognito-identity-js`).

## Practice Content
This practical section is divided into 2 main steps corresponding to the sub-folders:
* **4.3.1 Configuring Application and Sign-in Methods:** Set up the application type, identifier name, and user identity attributes (Email).
* **4.3.2 Completing Initialization and Retrieving Identity Parameters:** Create the User Directory, retrieve the User Pool ID and Client ID to embed into the frontend source code.

![Amazon Cognito User Pool Initialization Interface](/Workshop/images/4/4.3/2.1.png)
*Image Caption: Amazon Cognito management interface on the AWS Console.*

## Expected Results
* Successfully initialized the User Directory on Amazon Cognito in the `us-east-1` region.
* Successfully collected 2 important parameters: **User Pool ID** and **Client ID** to serve the frontend source code integration process in subsequent steps.