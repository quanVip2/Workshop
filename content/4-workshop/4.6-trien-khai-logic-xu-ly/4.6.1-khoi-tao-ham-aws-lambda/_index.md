---
title: "Initialize AWS Lambda Function"
weight: 1
pre: " <b> 4.6.1 </b> "
---

# INITIALIZE AWS LAMBDA FUNCTION

**Step 1: Create a New Lambda Function**

* From the AWS Management Console, search for and access the **Lambda** service. Ensure the Region is set to `us-east-1`.
* Click the orange **Create function** button.
* Select the **Author from scratch** option.

![alt text](/Workshop/images/4/4.5/image1.png)

**Step 2: Configure Basic Parameters**

* **Function name:** Name your function, for example: `HamXuLyAnh12`.
* **Runtime:** Select **Python 3.12** *(Note: You must select the correct version to ensure compatibility with the Pillow Layer in the next step)*.
* **Architecture:** Keep the default `x86_64`.

![alt text](/Workshop/images/4/4.5/image2.png)

**Step 3: Attach IAM Permissions (Execution Role)**

* Expand the **Additional settings** section.
* Select **Choose an existing role**.
* In the dropdown or search box below, select the IAM Role you created in the previous section, and click save.

![alt text](/Workshop/images/4/4.5/image3.png)

* Scroll down and click **Create function** for the system to initialize the virtual server.

![alt text](/Workshop/images/4/4.5/image4.png)