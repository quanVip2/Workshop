---
title: "2. API & AI Dashboard Integration"
weight: 2
pre: " <b> 4.11.2 </b> "
---

## 1. Embedding the API Gateway URL
The web browser does not call Lambda directly but through **API Gateway**.
1. Still in the `index.html` file, locate the API Gateway configuration section.
2. Paste the **Invoke URL** (which you copied in lesson 4.8) into the constants:
   * `API_GATEWAY_URL`: URL appended with `/get-upload-url` and `/get-download-url`
   * `API_HISTORY_URL`: URL appended with `/get-history`

## 2. Presenting the Analytics Dashboard
Instead of adding burden to the Backend, the `loadHistory()` function on the Frontend has been programmed to receive JSON data arrays from Lambda and automatically calculate metrics directly in the browser (Client-side rendering):
* **Total Images:** Counts the number of returned objects.
* **Total Original & Compressed Size:** Sums up the `KichThuocGoc` and `KichThuocNen` columns.
* **Savings Percentage:** Applies the formula `((Original - Compressed) / Original) * 100` to display the optimized bandwidth percentage.

## 3. Displaying Artificial Intelligence Tags (AI Tags)
Within the history table creation loop, the system extracts the `NhanDanAI` column from DynamoDB (analyzed by Amazon Rekognition) and prints it to the interface. If an image has no tags, the system displays `N/A`.

![alt text](/Workshop/images/4/4.11/2.4.png)
*Image Caption: Real-time capacity optimization statistics dashboard.*

![alt text](/Workshop/images/4/4.11/2.5.png)
*Image Caption: Rekognition Artificial Intelligence automatically tags image subjects.*