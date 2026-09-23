---
title: "Mở quyền truy cập công khai (Bucket Policy)"
weight: 2
pre: " <b> 4.8.2 </b> "
---

# MỞ QUYỀN TRUY CẬP CÔNG KHAI (BUCKET POLICY)

## Hướng dẫn chi tiết cách làm:
Mặc dù đã tắt "Block Public Access", AWS S3 vẫn mặc định cấm người lạ đọc nội dung bên trong trừ khi bạn cấp một "tờ giấy phép" (Policy) rõ ràng.

1. Chuyển sang thẻ **Permissions** (Quyền).

![alt text](/Workshop/images/4/4.8/image5.png)

2. Cuộn xuống mục **Bucket policy**, bấm **Edit**.

3. Dán đoạn mã JSON phân quyền công khai cho phép đọc dữ liệu vào khung soạn thảo.
![alt text](/Workshop/images/4/4.8/image6.png)

4. Bấm **Save changes** (Lưu thay đổi).


![alt text](/Workshop/images/4/4.8/image7.png)