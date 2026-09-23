---
title: "Blog 2"
weight: 3
pre: " <b> 3.2 </b> "
---

# INTEGRATING OBSERVABILITY FOR MICROSERVICES ON EKS WITH ADOT AND HELM

Observability is a vital factor in maintaining reliability within distributed system architectures. This solution provides a comprehensive monitoring deployment method for Microservices applications (specifically .NET) running on Amazon Elastic Kubernetes Service (EKS) by utilizing AWS Distro for OpenTelemetry (ADOT) combined with the Helm package manager.

## Key features of the solution:

* **Auto-instrumentation:** ADOT allows for the automatic extraction of telemetry data, including traces and metrics, without requiring any intervention or modification to the application source code (zero-code changes).
* **Standardized deployment with Helm and ADOT Operator:** Use Helm charts to package and deploy the ADOT Operator onto the Kubernetes cluster (EKS). This helps automate the lifecycle management process and flexibly provisions data collection configurations (Collector).
* **Deep integration with the AWS monitoring ecosystem:** After being processed by the ADOT Collector, telemetry data is seamlessly routed to **AWS X-Ray** (for distributed tracing analysis) and **Amazon CloudWatch** (for metrics monitoring).
* **Request Flow visualization:** Allows DevOps engineers to easily track the entire lifecycle of a request as it passes through multiple independent services (microservices), thereby accurately identifying performance bottlenecks.
* **Practical perspective for Computer Science:** This is a perfect demonstration of applying distributed system operation principles and automation practices (CI/CD/Infrastructure as Code), helping to reduce the Mean Time To Recovery (MTTR).

![Architecture diagram](/Workshop/images/anhblog3.2.jpg)

* **Link bài viết:** ([Blog cá nhân](https://lnkd.in/p/dtS99CXi))

* **Reference link:** [AWS Blog - Adding observability to .NET microservices on EKS with ADOT auto-instrumentation and Helm](https://aws.amazon.com/blogs/dotnet/adding-observability-to-net-microservices-on-eks-with-adot-auto-instrumentation-and-helm/)