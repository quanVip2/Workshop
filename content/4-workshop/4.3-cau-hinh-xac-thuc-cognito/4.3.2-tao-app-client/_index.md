---
title: "Completion and Parameter Retrieval"
weight: 2
pre: " <b> 4.3.2 </b> "
---

## Steps to Complete Initialization and Extract Parameters

**Step 5: Create User Directory**
* Review all configuration information from the previous steps.
* Scroll down to the bottom of the screen and click the orange **Create user directory** button.

![Click the create user directory button](/Workshop/images/4/4.3/2.5.png)

**Step 6: Extract User Pool ID and Client ID Parameters**
* Once the system completes the initialization (which takes a few seconds), you will be redirected to the dashboard of the newly created User Pool.
* **Checkpoint 1 (User Pool ID):** Look at the top section of the dashboard and copy the **User Pool ID** value (Formatted as `us-east-1_XXXXXXXXX`).
* **Checkpoint 2 (Client ID):** Scroll down the dashboard or click on the **App Clients** tab, locate the App client list section to copy the **Client ID** string of the newly created SPA application.

![User Pool ID](/Workshop/images/4/4.3/2.6.png)
![Client ID](/Workshop/images/4/4.3/2.7.png)

After completing this step, we are ready to move on to building the S3 storage infrastructure in the next lesson!