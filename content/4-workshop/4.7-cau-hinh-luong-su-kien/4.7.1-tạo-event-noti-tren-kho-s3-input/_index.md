---
title: "Create Event Notification on S3 Input Bucket"
weight: 1
pre: " <b> 4.7.1 </b> "
---

**Step 1: Access the Source Image Bucket Settings**
1. From the AWS Console search bar, reopen the **S3** service.
2. In the list of Buckets, click on the correct bucket `kho-anh-goc-cua-toi-1` (Input Bucket).
3. Switch to the **Properties** tab.

![alt text](/images/4/4.7/image1.png)

**Step 2: Configure Event Parameters**
1. Scroll down to find the **Event notifications** section.
2. Click the **Create event notification** button.

![alt text](/images/4/4.7/image2.png)

3. **Event name:** Enter a name for easy management, for example: `HamXuLyAnh`.
4. **Prefix / Suffix:** Leave blank to apply to all uploaded files.

![alt text](/images/4/4.7/image3.png)

**Step 3: Select Trigger Event Types**
* In the **Event types** section, check the box for **All object create events**.

![alt text](/images/4/4.7/image4.png)

**Step 4: Specify Destination**
1. Scroll down to the bottom to the **Destination** section.
2. Select the **Lambda function** option.
3. In the **Specify Lambda function** dropdown, the system will automatically list your available functions. Select the `HamXuLyAnh12` function that you wrote the Python source code for earlier.
4. Click the **Save changes** button at the bottom right.

![alt text](/images/4/4.7/image5.png)
![alt text](/images/4/4.7/image6.png)