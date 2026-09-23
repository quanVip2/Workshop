---
title: "System Access Authorization"
weight: 5
pre: " <b> 4.5 </b> "
---

## Objectives
Establish identity and assign secure access permissions for components in the Serverless architecture. Ensure the AWS Lambda function has valid authority to read/write images with Amazon S3, log metadata into Amazon DynamoDB, and output execution logs to Amazon CloudWatch.

## Overview
In Cloud-Native architecture, security is a top priority. AWS IAM (Identity and Access Management) is the service used to solve the authorization problem without directly embedding passwords or access keys into the backend source code.

Instead of using a Root account with full privileges (which is highly risky), this workshop applies the fundamental security Principle of Least Privilege. We will create a virtual identity (IAM Role) dedicated to AWS Lambda. The Lambda service will "assume" this identity during runtime to interact with other AWS services safely and completely automatically.

## Practice Content
This practice section includes two main procedures:

* Initialize a new IAM Role and specify AWS Lambda as the entity allowed to use this Role (Trusted Entity).
* Attach Policies to grant read/write permissions for S3, query permissions for DynamoDB, and logging permissions for CloudWatch.

## Expected Outcomes
* A new IAM Role is successfully created on the system.
* This Role contains exactly the 3 required Policies.
* The Role is in a ready state to be attached to the AWS Lambda function in the subsequent deployment steps.