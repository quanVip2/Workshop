---
title: "Blog 3"
weight: 3
pre: " <b> 3.3 </b> "
---

# CHUYỂN ĐỔI AI AGENTS ĐA MÔ HÌNH SANG AMAZON BEDROCK

Việc xây dựng các trợ lý trí tuệ nhân tạo (AI Agents) tinh vi thường đòi hỏi sự kết hợp của nhiều mô hình nền tảng (Foundation Models - FMs) khác nhau để xử lý các tác vụ chuyên biệt. Tuy nhiên, việc tự quản lý và điều phối luồng giao tiếp giữa các mô hình này tạo ra rào cản lớn về hạ tầng. Bài viết này phân tích phương pháp di chuyển (migrate) kiến trúc AI Agents đa mô hình tự quản lý sang dịch vụ được quản lý hoàn toàn **Amazon Bedrock Agents** và **Core Runtime**.

## Các điểm chính của giải pháp:

* **Đơn giản hóa công tác điều phối (Orchestration):** Thay vì phải tự xây dựng các khung logic phức tạp để quản lý chuỗi suy luận của AI, Amazon Bedrock Agents tự động phân tích ngôn ngữ tự nhiên, chia nhỏ tác vụ và quyết định gọi các API hoặc truy xuất dữ liệu phù hợp (ReAct prompting).
* **Tính linh hoạt đa mô hình (Multi-Model Flexibility):** Bedrock Core Runtime cho phép các nhà phát triển dễ dàng chuyển đổi hoặc kết hợp nhiều mô hình hàng đầu (như Anthropic Claude, Amazon Titan, Meta Llama) trong cùng một luồng công việc để tối ưu hóa chi phí và hiệu suất cho từng tác vụ cụ thể (ví dụ: mô hình nhẹ để định tuyến, mô hình mạnh để tạo văn bản).
* **Tích hợp liền mạch với Knowledge Bases:** Đơn giản hóa việc triển khai kiến trúc RAG (Retrieval-Augmented Generation) bằng cách kết nối trực tiếp Agent với các kho dữ liệu doanh nghiệp, giúp AI đưa ra câu trả lời chính xác, có ngữ cảnh và giảm thiểu hiện tượng ảo giác (hallucination).
* **Tối ưu hóa vận hành và Bảo mật:** Loại bỏ hoàn toàn gánh nặng quản lý máy chủ (Serverless AI). Dữ liệu khách hàng và dữ liệu huấn luyện được giữ an toàn trong môi trường VPC, tuân thủ các tiêu chuẩn bảo mật khắt khe của AWS.
* **Góc nhìn thực tiễn cho Khoa học Máy tính:** Quá trình chuyển đổi này cung cấp bài học quan trọng về thiết kế kiến trúc phần mềm tích hợp AI (AI-integrated Software Architecture). Nó minh họa xu hướng dịch chuyển từ việc phát triển mô hình cục bộ sang tận dụng các nền tảng quản lý MLOps/LLMOps trên đám mây để mở rộng quy mô.

![Kiến trúc Amazon Bedrock Agents](/Workshop/images/baiblog3.3.png)

* **Link bài viết:** ([Blog cá nhân](https://lnkd.in/p/dcQ8E83M))
* **Link tham khảo:** [AWS Blog - Migrating multi-model AI agents to Amazon Bedrock Agent/Core Runtime](https://aws.amazon.com/blogs/machine-learning/migrating-multi-model-ai-agents-to-amazon-bedrock-agentcore-runtime/)