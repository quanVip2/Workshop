---
title: "3. Setting up Routes & Integrations"
weight: 3
pre: " <b> 4.8.3 </b> "
---

## Routing APIs to Lambda

We need to create 3 routes for the frontend to call, then attach authorization tags and specify the Lambda function (integration) that will handle them.

**Step 1: Create Routes**
1. Select the **Routes** menu on the left. Click **Create**.
2. Select the method as **GET**, enter the path: `/get-upload-url` -> Click **Create**.
3. Repeat similarly to create 2 more routes:
   * Method **GET**, path: `/get-history`
   * Method **GET**, path: `/get-download-url`

**Step 2: Attach Security and Connect Lambda**
1. Click on the newly created **`GET /get-upload-url`** route.
2. Under the **Authorization** section on the right, click **Attach authorization**. Select `CognitoAuth` (created in the previous section) and click **Attach**.
3. Under the **Integration** section on the right, click **Attach integration** -> Select **Create and attach an integration**.
   * Integration type: Select **Lambda function**.
   * Integration details: Select the **`GenerateUploadUrl`** function.
   * Click **Create**.

**Step 3: Repeat the process for the remaining 2 routes**
* For **`GET /get-history`**: Attach `CognitoAuth` security and connect to the **`GetUserHistory`** Lambda function.
* For **`GET /get-download-url`**: Attach `CognitoAuth` security and connect to the **`GenerateDownloadUrl`** Lambda function.

*(Never connect the `HamXuLyAnh` function here).*

![Connecting Routes with Security Layer and Backend](/Workshop/images/4/4.8/2.3.png)

![Connecting Routes with Security Layer and Backend](/Workshop/images/4/4.8/2.4.png)