---
title: "Building API Gateway"
weight: 8
pre: " <b> 4.8 </b> "
---

## Objectives
Set up **Amazon API Gateway** to act as the "Front Door" for the Web Frontend interface to communicate securely with the backend system. 

## API Architecture Overview
In our Enterprise Serverless system, the frontend must never call the Database or S3 directly. Instead, it must go through API Gateway. 
API Gateway performs 2 critical tasks:
1. **Security Screening:** Blocks unauthorized users by checking the `JWT Token` through a Cognito Authorizer.
2. **Routing:** Channels requests (Upload, Get History, Download) to their corresponding AWS Lambda functions for processing.

*(Note: The `HamXuLyAnh` function will not be connected to API Gateway because it runs as a background job via an S3 Trigger event).*

## Practical Content
We will divide the API Gateway setup process into 4 phases corresponding to 4 small labs:
* **4.8.1 Initializing HTTP API:** Build the foundational API framework.
* **4.8.2 Configuring Cognito JWT Authorizer:** Integrate the token-based protection layer.
* **4.8.3 Setting up Routes & Integrations:** Create 3 routes connected to 3 Lambda functions.
* **4.8.4 Configuring CORS & Getting URL:** Unlock browser communication and complete deployment.

![The central role of Amazon API Gateway in the system](/Workshop/images/so_do.png)