---
title: "Phân tích thông số hiệu suất (Timeout/Memory)"
weight: 2
pre: " <b> 4.9.2 </b> "
---

## Hướng dẫn chi tiết cách làm:

**Bước 1: Đọc cấu trúc của một phiên chạy**
Khi mở Log stream, bạn sẽ thấy hàng loạt các dòng văn bản. Một phiên thực thi thành công của Lambda sẽ luôn có cấu trúc 3 phần bắt buộc:
* `START RequestId: ...` (Bắt đầu nhận sự kiện từ S3).
* Các dòng Log do code Python sinh ra (nếu có lỗi, chi tiết lỗi sẽ in màu đỏ ở khu vực này).
* `END RequestId: ...` (Kết thúc xử lý).
* `REPORT RequestId: ...` (Báo cáo tổng kết chỉ số hệ thống).

**Bước 2: Phân tích dòng REPORT (Bằng chứng tối ưu hóa)**
Hãy chú ý vào dòng chữ bắt đầu bằng chữ `REPORT` và phân tích 2 chỉ số cực kỳ quan trọng sau:

1. **Duration (Thời gian thực thi):** 
   * *Đánh giá:* Thời gian này thấp hơn rất nhiều so với giới hạn Timeout: 15.00 seconds mà chúng ta đã thiết lập ở cấu hình Lambda. Nghĩa là hệ thống chạy an toàn, không bị ép ngắt giữa chừng.
   ![alt text](/images/4/4.9/image3.png)
2. **Max Memory Used (Bộ nhớ tối đa đã dùng):** 
   * *Đánh giá:* Mặc định Lambda chỉ cho 128 MB. Nếu chúng ta không chủ động tăng Memory Size lên 512 MB ở chương trước, hàm này chắc chắn đã bị Crash (sập) vì tràn RAM do thư viện Pillow nén ảnh tốn khá nhiều bộ nhớ.

![alt text](/images/4/4.9/image4.png)