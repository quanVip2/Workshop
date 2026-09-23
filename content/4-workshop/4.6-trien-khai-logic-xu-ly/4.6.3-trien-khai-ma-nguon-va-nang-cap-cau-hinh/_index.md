---
title: "Deploying Source Code and Upgrading Server Configuration"
weight: 3
pre: " <b> 4.6.3 </b> "
---

# DEPLOYING SOURCE CODE AND UPGRADING SERVER CONFIGURATION

## Detailed Instructions:

**Step 1: Enhance Computing Power (Optimize Performance)**
By default, Lambda only allocates 128MB of RAM and 3 seconds of processing time. This is insufficient for the Pillow library to compress images, causing Crash errors (Timeout).
1. Switch to the **Configuration** tab ➔ Select **General configuration** from the left menu.
![alt text](/images/4/4.5/image8.png)
2. Click the **Edit** button.
3. Increase **Memory (RAM)** to **512 MB**.
4. Increase **Timeout** to **15 seconds**.
5. Click **Save**.
![alt text](/images/4/4.5/image9.png)

**Step 2: Deploy Python Source Code (Code Deploy)**
1. Return to the **Code** tab.
2. In the **Code source** editor, delete all default code and paste the processing code.
![alt text](/images/4/4.5/image10.png)

**Step 3: Save and Update (Extremely Important)**
1. Click the light gray **Deploy** button located above the code editor.
2. *Note:* If you skip this step, AWS Lambda will not save the new code configuration and will still run the default sample code, leading to an unresponsive system. Wait for the green success message "Successfully updated the function" to appear to complete.

![alt text](/images/4/4.5/image11.png)