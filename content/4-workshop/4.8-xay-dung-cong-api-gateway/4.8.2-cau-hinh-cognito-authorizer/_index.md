---
title: "2. Configuring Cognito JWT Authorizer"
weight: 2
pre: " <b> 4.8.2 </b> "
---

## Integrating the Cognito Protection Layer

This is a critical step that helps API Gateway know how to "read" the Token sent by the user to determine whether they have logged in successfully or not.

**Implementation Steps:**
1. In your API management page (`ImageProcessorAPI`), look at the left-hand menu and select **Authorization**.
2. Switch to the **Manage authorizers** tab and click **Create**.
3. Configure the following parameters:
   * **Authorizer type:** Choose **JWT**.
   * **Name:** Enter `CognitoAuth`.
   * **Identity source:** Enter `$request.header.Authorization` (The browser will send the Token in this Header).
   * **Issuer URL:** Paste your User Pool issuer URL. The standard format is: 
     `https://cognito-idp.us-east-1.amazonaws.com/<YOUR_USER_POOL_ID>` 
     *(Replace the ID string you copied in lesson 4.3 here)*.
   * **Audience:** Paste the **Client ID** (App Client) string you copied in lesson 4.3 here.
4. Click **Create** to save this protection layer.

![Creating a JWT Authorizer linked with Amazon Cognito](/Workshop/images/4/4.8/2.2.png)