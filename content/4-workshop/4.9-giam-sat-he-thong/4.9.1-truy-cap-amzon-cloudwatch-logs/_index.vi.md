---
title: "Truy cập Amazon CloudWatch Logs"
weight: 1
pre: " <b> 4.9.1 </b> "
---


## Hướng dẫn chi tiết cách làm:

**Bước 1: Đi từ giao diện Lambda (Cách nhanh nhất)**
1. Mở lại dịch vụ **Lambda** trên AWS Console và chọn hàm `HamXuLyAnh12`  của bạn.
2. Chuyển sang thẻ **Monitor** (Giám sát).
3. Bấm vào nút **View CloudWatch logs** (Xem nhật ký CloudWatch). Hệ thống sẽ tự động mở một tab mới và đưa bạn đến đúng thư mục chứa log của hàm này (được gọi là Log group: `/aws/lambda/HamXuLyAnh12`).

![alt text](/Workshop/images/4/4.9/image1.png)

**Bước 2: Chọn luồng sự kiện (Log stream)**
1. Tại giao diện CloudWatch vừa mở ra, cuộn xuống phần **Log streams** (Luồng nhật ký).
2. Hệ thống sẽ liệt kê các phiên chạy theo thời gian. Hãy nhấp vào dòng trên cùng (Luồng log mới nhất - tương ứng với bức ảnh bạn vừa tải lên ở bước thử nghiệm Web).

![alt text](/Workshop/images/4/4.9/image2.png)