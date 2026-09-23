---
title: "Enable Public Access (Bucket Policy)"
weight: 2
pre: " <b> 4.8.2 </b> "
---

# ENABLE PUBLIC ACCESS (BUCKET POLICY)

## Detailed Instructions:
Even though "Block Public Access" has been turned off, AWS S3 still defaults to blocking strangers from reading the contents inside unless you explicitly grant a "permit" (Policy).

1. Switch to the **Permissions** tab.

![alt text](/Workshop/images/4/4.8/image5.png)

2. Scroll down to the **Bucket policy** section and click **Edit**.

3. Paste the JSON snippet for public read permissions into the editor.

![alt text](/Workshop/images/4/4.8/image6.png)

4. Click **Save changes**.

![alt text](/Workshop/images/4/4.8/image7.png)