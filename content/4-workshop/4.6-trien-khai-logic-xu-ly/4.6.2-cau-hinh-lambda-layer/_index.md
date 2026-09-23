---
title: "Configure Lambda Layer (Pillow Library)"
weight: 2
pre: " <b> 4.6.2 </b> "
---

In a practical environment, using third-party ARN codes (Klayers) requires absolute synchronization regarding Version and Region.

1. On the management page for the `HamXuLyAnh12` function, scroll down to the bottom to find the **Layers** section and click **Add a layer** (or **Edit**).

![alt text](/images/4/4.5/image5.png)

2. Click the **Add a layer** button.

3. Select the **Specify an ARN** option.

![alt text](/images/4/4.5/image6.png)

4. Since the AWS system continuously cleans up older versions, you need to paste the ARN code of the Klayers repository compatible with Python 3.12/3.14 in `us-east-1` (looked up from the Klayers project GitHub):
   `arn:aws:lambda:us-east-1:770693421928:layer:Klayers-p314-Pillow:3`
5. Click the **Verify** button. If no red error box appears and the library description information `pillow==12.3.0` is displayed, click **Add** to finish and click **Save** to save.

![alt text](/images/4/4.5/image7.png)