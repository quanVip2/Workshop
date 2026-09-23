---
title: "Blog 2"
weight: 3
pre: " <b> 3.2 </b> "
---

# TÍCH HỢP KHẢ NĂNG QUAN SÁT CHO MICROSERVICES TRÊN EKS VỚI ADOT VÀ HELM

Khả năng quan sát (Observability) là yếu tố sống còn để duy trì độ tin cậy trong các kiến trúc hệ thống phân tán. Giải pháp này cung cấp phương pháp triển khai giám sát toàn diện cho các ứng dụng Microservices (cụ thể là .NET) chạy trên Amazon Elastic Kubernetes Service (EKS) bằng cách sử dụng AWS Distro for OpenTelemetry (ADOT) kết hợp với công cụ quản lý gói Helm.

## Các điểm chính của giải pháp:

* **Thu thập dữ liệu tự động (Auto-instrumentation):** ADOT cho phép tự động trích xuất các dữ liệu viễn trắc (telemetry data) bao gồm traces và metrics mà không cần can thiệp hay sửa đổi mã nguồn ứng dụng (zero-code changes).
* **Triển khai chuẩn hóa với Helm và ADOT Operator:** Sử dụng Helm charts để đóng gói và triển khai ADOT Operator lên cụm Kubernetes (EKS). Việc này giúp tự động hóa quá trình quản lý vòng đời và cấp phát các cấu hình thu thập dữ liệu (Collector) một cách linh hoạt.
* **Tích hợp sâu với hệ sinh thái giám sát AWS:** Dữ liệu viễn trắc sau khi được ADOT Collector xử lý sẽ được định tuyến liền mạch đến **AWS X-Ray** (để phân tích dấu vết phân tán - distributed tracing) và **Amazon CloudWatch** (để theo dõi số liệu metrics).
* **Trực quan hóa luồng dữ liệu (Request Flow):** Cho phép các kỹ sư DevOps dễ dàng theo dõi toàn bộ vòng đời của một yêu cầu (request) khi nó đi qua nhiều dịch vụ độc lập (microservices), từ đó xác định chính xác nút thắt cổ chai (bottlenecks) về hiệu suất.
* **Góc nhìn thực tiễn cho Khoa học Máy tính:** Đây là một minh chứng hoàn hảo về ứng dụng các nguyên lý vận hành hệ thống phân tán và thực hành tự động hóa (CI/CD/Infrastructure as Code), giúp rút ngắn thời gian phát hiện và khắc phục sự cố (MTTR - Mean Time To Recovery).

![Sơ đồ kiến trúc ](/images/anhblog3.2.jpg)

* **Link bài viết:** ([Blog cá nhân](https://lnkd.in/p/dtS99CXi))
* **Link tham khảo:** [AWS Blog - Adding observability to .NET microservices on EKS with ADOT auto-instrumentation and Helm](https://aws.amazon.com/blogs/dotnet/adding-observability-to-net-microservices-on-eks-with-adot-auto-instrumentation-and-helm/)