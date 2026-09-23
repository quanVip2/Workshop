---
title: "Cấp quyền truy cập hệ thống"
weight: 5
pre: " <b> 4.5 </b> "
---

## Mục tiêu
Thiết lập danh tính và phân quyền truy cập an toàn cho các thành phần trong kiến trúc Serverless. Đảm bảo hàm AWS Lambda có đủ thẩm quyền hợp lệ để đọc/ghi ảnh với Amazon S3, ghi chép siêu dữ liệu (metadata) vào Amazon DynamoDB và xuất nhật ký hoạt động (logs) ra Amazon CloudWatch.

## Tổng quan
Trong kiến trúc Điện toán đám mây (Cloud-Native), bảo mật là ưu tiên hàng đầu. AWS IAM (Identity and Access Management) là dịch vụ được sử dụng để giải quyết bài toán cấp quyền mà không cần nhúng trực tiếp mật khẩu hay khóa truy cập vào mã nguồn backend.

Thay vì sử dụng tài khoản Root có toàn quyền (rất rủi ro), workshop này áp dụng nguyên tắc Bảo mật cơ bản (Principle of Least Privilege - Quyền hạn tối thiểu). Chúng ta sẽ tạo ra một "Vai trò ảo" (IAM Role) dành riêng cho AWS Lambda. Dịch vụ Lambda sẽ "đóng vai" (assume) định danh này trong lúc chạy để tương tác với các dịch vụ AWS khác một cách an toàn và hoàn toàn tự động.

## Nội dung thực hành
Phần thực hành này bao gồm hai quy trình chính:

* Khởi tạo một IAM Role mới và chỉ định AWS Lambda là thực thể được phép sử dụng Role này (Trusted Entity).
* Gắn các bộ quy tắc (Policies) để cấp quyền đọc/ghi S3, truy vấn DynamoDB và ghi Log lên CloudWatch.

## Kết quả mong đợi
* Một IAM Role mới được tạo thành công trên hệ thống.
* Role này chứa chính xác 3 quyền hạn (Policies) cần thiết.
* Role ở trạng thái sẵn sàng để được gắn vào hàm AWS Lambda ở các bước triển khai tiếp theo.