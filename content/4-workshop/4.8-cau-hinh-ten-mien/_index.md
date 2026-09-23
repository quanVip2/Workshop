---
title: "Domain and Web Hosting Configuration (Deploying Static Interface on S3)"
weight: 7
pre: " <b> 4.8 </b> "
---

## Objectives
Publish the Frontend source code file (`index.html`) to the Internet so that any device can access it via a single Endpoint URL. Ensure the web interface operates smoothly 24/7 without the need to rent or configure traditional web servers.

## Overview
To turn the practical exercise into a production-ready product, users cannot constantly download the `index.html` file to their computers to run it. In conventional systems, engineers would have to rent a server (such as Amazon EC2), install Nginx/Apache, configure domain names, etc., which is complex and costly.

However, with Serverless architecture, we utilize a fantastic feature of Amazon S3 called **Static Website Hosting**. This feature turns a standard S3 bucket into an ultra-fast static web server with infinite scalability and a free public link provided out of the box. This helps the project achieve maximum cost-optimization criteria.

## Practice Content
This practice section includes three main procedures:

* Create a new S3 bucket dedicated to the web interface and enable the Static Website Hosting feature.
* Set up a security policy (Bucket Policy) allowing public access so anyone can view the website.
* Upload the `index.html` file to the system and retrieve the Endpoint URL (AWS default domain name) for use.

## Expected Outcomes
* A new S3 bucket is initialized to act as a Web server.
* The image processing website is accessible from anywhere via the Internet (on both PC and Mobile) using the Endpoint URL.
* The browser successfully loads the interface and the Javascript AWS SDK scripts to communicate directly with the backend infrastructure.