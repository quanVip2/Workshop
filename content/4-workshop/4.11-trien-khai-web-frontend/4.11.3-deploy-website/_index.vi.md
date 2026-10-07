---
title: "3. Triển khai Website (Public URL)"
weight: 3
pre: " <b> 4.11.3 </b> "
---

## Đưa dự án lên môi trường Internet
Sau khi hoàn tất cấu hình và chạy thử trên máy tính cá nhân (Localhost) thành công, bước cuối cùng là triển khai giao diện lên môi trường Internet để hội đồng chấm điểm và người dùng thực tế có thể truy cập.

Chúng ta sử dụng giải pháp **Netlify** (hoặc AWS S3 Static Website Hosting) vì tính năng CI/CD tự động, hỗ trợ HTTPS miễn phí và hoàn toàn Serverless.

**Các bước thực hiện (Triển khai cực tốc với Netlify Drop):**
1. Đảm bảo toàn bộ mã nguồn của bạn (`index.html`, các thư mục CSS, JS nếu có) đã được lưu lại trong thư mục `Enterprise_Image_Processor`.
2. Truy cập trang web: [https://app.netlify.com/drop](https://app.netlify.com/drop)
3. Kéo và thả nguyên thư mục dự án của bạn vào vòng tròn tải lên.
4. Chờ 3 giây, Netlify sẽ tự động cung cấp cho bạn một đường dẫn (Public URL) công khai có chứng chỉ bảo mật HTTPS (Ví dụ: `https://image-processor-pro.netlify.app`).


![alt text](/Workshop/images/4/4.11/2.6.png)

*Chú thích ảnh: Triển khai Frontend lên môi trường Internet công khai.*