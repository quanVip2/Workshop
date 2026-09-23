---
title: "Cấu hình Lambda Layer (Thư viện Pillow)"
weight: 2
pre: " <b> 4.6.2 </b> "
---

Trong môi trường thực hành, việc sử dụng mã ARN của bên thứ ba (Klayers) yêu cầu sự đồng bộ tuyệt đối về phiên bản (Version) và Khu vực (Region).

1. Tại trang quản lý hàm `HamXuLyAnh12`, cuộn màn hình xuống dưới cùng tìm khu vực **Layers** (Lớp) bấm vào Edit 

![alt text](/images/4/4.5/image5.png)

2. Nhấn nút **Add a layer** (Thêm lớp)

3. Chọn tùy chọn **Specify an ARN** (Chỉ định ARN).

![alt text](/images/4/4.5/image6.png)

4. Do hệ thống AWS liên tục dọn dẹp các phiên bản cũ, bạn cần dán đoạn mã ARN của kho Klayers tương thích với Python 3.14 tại `us-east-1` (đã được tra cứu từ GitHub của dự án Klayers): 
   `arn:aws:lambda:us-east-1:770693421928:layer:Klayers-p314-Pillow:3`
5. Nhấn nút **Verify** (Xác minh). Nếu khung báo lỗi màu đỏ không xuất hiện và hiện ra thông tin mô tả thư viện `pillow==12.3.0`, hãy nhấn **Add** (Thêm) để hoàn tất và bấm save để lưu
![alt text](/images/4/4.5/image7.png)
