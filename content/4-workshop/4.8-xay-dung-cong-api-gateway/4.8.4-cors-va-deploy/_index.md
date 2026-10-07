---
title: "4. Configuring CORS and Completion"
weight: 4
pre: " <b> 4.8.4 </b> "
---

## Unlocking Communication (CORS) and Getting the API URL

Since the Web Frontend and API Gateway (Backend) reside on different domains, the browser will block connections by default. We must configure CORS to allow the data flow to pass through.

**Step 1: Configure CORS**
* Look at the left-hand menu, under the *Develop* section, select **CORS**.
* Click **Configure** and enter the following parameters:
  * **Access-Control-Allow-Origins:** Enter `*` (or your website's domain) -> Click Add.
  * **Access-Control-Allow-Headers:** Enter `*` or `Authorization, Content-Type` -> Click Add.
  * **Access-Control-Allow-Methods:** Enter `*` or select `GET, OPTIONS` -> Click Add.
  * **Access-Control-Expose-Headers:** Leave blank.
  * **Max-age:** Enter `300`.
* Click **Save** to save.

![Configuring CORS to allow Frontend to communicate with API](/Workshop/images/4/4.8/2.5.png)

**Step 2: Get the URL to Configure the Frontend**
* Select the **API: ImageProcessorAPI** menu (click on the text at the top left to return to the API dashboard).
* Under the **Invoke URL** section, you will see a path formatted like:
  `https://xxxxxxxxx.execute-api.us-east-1.amazonaws.com`
* Copy this path. This is the backbone for connecting your interface to the entire AWS system. You will use this link to assign to the `API_GATEWAY_URL` and `API_HISTORY_URL` variables in the Javascript source code in subsequent sections.

![Copying Invoke URL to attach to Frontend](/Workshop/images/4/4.8/2.6.png)