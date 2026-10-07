---
title: "1. Authentication Configuration (Cognito UI)"
weight: 1
pre: " <b> 4.11.1 </b> "
---

## Embedding Amazon Cognito Parameters into Source Code

For the Sign In / Sign Up web form to communicate with the User Pool created in lesson 4.3, we need to declare the parameters.

**Implementation Steps:**
1. Open the project's `index.html` file using Visual Studio Code.
2. Locate the beginning of the `<script>` tag, where you will find the Cognito Configuration declaration area.
3. Replace the placeholder values with the parameters you saved:
   * `POOL_ID`: Enter the **User Pool ID** value (e.g., `us-east-1_xxxxxxxxx`).
   * `CLIENT_ID`: Enter the **App Client ID** value (e.g., `3abc123...`).
   * `REGION`: Declare `'us-east-1'`.

**Dynamic Form Interface:**
The frontend system has been pre-programmed with a `toggleAuth()` function to automatically change the `<h1>` title to *"Sign In"* or *"Create Account"* depending on the user's action, providing a seamless experience.

![alt text](/Workshop/images/4/4.11/2.2.png)
*Image Caption: Declaring Amazon Cognito parameters in the frontend.*

![alt text](/Workshop/images/4/4.11/2.3.png)
*Image Caption: Account registration interface authenticated via Cognito.*