---
title: "Create a Dedicated S3 Bucket for the Website and Enable Hosting"
weight: 1
pre: " <b> 4.8.1 </b> "
---

**Step 1: Create the Web Storage Bucket**
1. Access the **S3** service on the AWS Console.
2. Click **Create bucket**.
3. **AWS Region:** Select `us-east-1` (N. Virginia).
4. **Bucket name:** Choose an easy-to-remember name (For example: `trang-web-xu-ly-anh-cua-toi`). This bucket will be completely independent of the previously created Input and Output buckets.

![alt text](/Workshop/images/4/4.8/image1.png)

5. Scroll down to the **Block Public Access settings for this bucket** section. Uncheck (turn off) the **Block all public access** box.
6. A yellow warning will appear; check the box for *"I acknowledge that the current settings..."* to confirm that you intentionally intend to make this bucket public (since it is a public website).

![alt text](/Workshop/images/4/4.8/image2.png)

7. Scroll to the bottom and click **Create bucket**.


**Step 2: Enable the Web Server Feature (Static Website Hosting)**
1. In the list of Buckets, click on the newly created `trang-web-xu-ly-anh-cua-toi` bucket.
2. Switch to the **Properties** tab.
3. Scroll down to the very bottom, find the **Static website hosting** section, and click **Edit**.

![alt text](/Workshop/images/4/4.8/image3.png)

4. Select **Enable**.
5. In the **Index document** field, enter the exact name of your source code file: `index.html`.
6. Click **Save changes**.

![alt text](/Workshop/images/4/4.8/image4.png)