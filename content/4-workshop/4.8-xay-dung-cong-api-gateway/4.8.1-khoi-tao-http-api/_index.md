---
title: "1. Initializing HTTP API"
weight: 1
pre: " <b> 4.8.1 </b> "
---

## Initializing Foundational API Gateway

There are several types of APIs in AWS API Gateway (REST API, HTTP API, WebSocket). For modern SPA web architectures and cost optimization, we will use the **HTTP API** protocol.

**Implementation Steps:**
1. Access the **API Gateway** service on the AWS Console.
2. Click the **Create API** button.
3. Under the **HTTP API** section, click the **Build** button.
4. Declare basic information:
   * **API name:** Enter `ImageProcessorAPI` (Or any name you prefer).
   * Skip the "Add integrations" section in this step (We will add details later).
   * Click **Next**.
5. **Configure routes** section: Keep it blank and click **Next**.
6. **Define stages** section: Keep the default stage as `$default` (auto-deploy) and click **Next**.
7. Review information and click **Create**.

![Initializing HTTP API on AWS](/Workshop/images/4/4.8/2.1.png)
 
*Image Caption: Initializing HTTP API on AWS.*