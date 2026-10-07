---
title: "3. Website Deployment (Public URL)"
weight: 3
pre: " <b> 4.11.3 </b> "
---

## Publishing the Project to the Internet
After completing the configuration and successfully testing on your local computer (Localhost), the final step is to deploy the interface to the Internet so that the evaluation committee and actual users can access it.

We use **Netlify** (or AWS S3 Static Website Hosting) because of its automated CI/CD features, free HTTPS support, and completely serverless nature.

**Implementation Steps (Lightning-fast deployment with Netlify Drop):**
1. Ensure all your source code (`index.html`, CSS, and JS folders if any) is saved inside the `Enterprise_Image_Processor` folder.
2. Visit the website: [https://app.netlify.com/drop](https://app.netlify.com/drop)
3. Drag and drop your entire project folder into the upload circle.
4. Wait 3 seconds, and Netlify will automatically provide you with a public URL with an HTTPS security certificate (e.g., `https://image-processor-pro.netlify.app`).

![alt text](/Workshop/images/4/4.11/2.6.png)

*Image Caption: Deploying the frontend to a public Internet environment.*