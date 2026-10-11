---
title: "1. Khởi tạo HTTP API"
weight: 1
pre: " <b> 4.8.1 </b> "
---

## Khởi tạo API Gateway nền tảng

Trong AWS API Gateway có nhiều loại (REST API, HTTP API, WebSocket). Đối với kiến trúc Web SPA hiện đại và để tối ưu chi phí, chúng ta sẽ sử dụng giao thức **HTTP API**.

**Các bước thực hiện:**
1. Truy cập dịch vụ **API Gateway** trên AWS Console.
2. Nhấn nút **Create API** (Tạo API).
3. Tại mục **HTTP API**, nhấn nút **Build**.
4. Khai báo thông tin cơ bản:
   * **API name:** Nhập tên `ImageProcessorAPI` (Hoặc tên tùy ý bạn muốn).
   * Bỏ qua phần "Add integrations" ở bước này (Chúng ta sẽ thêm chi tiết sau).
   * Nhấn **Next**.
5. Phần **Configure routes**: Giữ trống và nhấn **Next**.
6. Phần **Define stages**: Giữ nguyên stage mặc định là `$default` (tự động triển khai) và nhấn **Next**.
7. Xem lại thông tin và nhấn **Create**.

![Khởi tạo HTTP API trên AWS](/Workshop/images/4/4.8/2.1.png)
 
