---
title: "Access Amazon CloudWatch Logs"
weight: 1
pre: " <b> 4.9.1 </b> "
---


## Detailed Instructions:

**Step 1: Navigate from the Lambda Interface (Fastest Way)**
1. Reopen the **Lambda** service on the AWS Console and select your `HamXuLyAnh12` function.
2. Switch to the **Monitor** tab.
3. Click the **View CloudWatch logs** button. The system will automatically open a new tab and take you directly to the folder containing logs for this function (called the Log group: `/aws/lambda/HamXuLyAnh12`).

![alt text](/images/4/4.9/image1.png)

**Step 2: Select the Event Log Stream**
1. In the opened CloudWatch interface, scroll down to the **Log streams** section.
2. The system will list execution sessions by timestamp. Click on the top row (the newest log stream, corresponding to the image you just uploaded in the web testing step).

![alt text](/images/4/4.9/image2.png)