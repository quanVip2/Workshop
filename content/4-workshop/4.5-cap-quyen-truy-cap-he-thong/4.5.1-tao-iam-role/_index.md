---
title: "Create IAM Role"
weight: 1
pre: " <b> 4.5.1 </b> "
---
# CREATE IAM ROLE

**Step 1: Access the IAM Dashboard**
1. In the top search bar of the AWS Management Console interface, type **IAM** and select the IAM service (Manage access to AWS resources).
2. In the left navigation menu, click on the **Roles** option.

![alt text](/images/4/4.4/image1.png)

**Step 2: Start Creating a Role**
1. Click the orange **Create role** button located in the top right corner.
2. The system will switch to the Select trusted entity setup interface. This is the step where the AWS system asks you: "Who or what service is allowed to use this permission?".

![alt text](/images/4/4.4/image2.png)

**Step 3: Select Trusted Service**
1. Under the **Trusted entity type** section, select the **AWS service** box.
2. Under the **Use case** section, select **Lambda** from the list of common services (or search for "Lambda" in the search box).
3. Click the **Next** button at the bottom right to proceed to the permissions step.

![alt text](/images/4/4.4/image3.png)