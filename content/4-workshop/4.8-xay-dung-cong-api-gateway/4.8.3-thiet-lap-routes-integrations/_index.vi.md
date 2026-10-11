---
title: "3. Thiết lập Routes & Integrations"
weight: 3
pre: " <b> 4.8.3 </b> "
---

## Định tuyến API đến Lambda

Chúng ta cần tạo 3 con đường (Routes) để Frontend gọi lên, sau đó gắn thẻ bảo vệ (Authorization) và chỉ định hàm Lambda (Integration) sẽ xử lý.

**Bước 1: Tạo Routes**
1. Chọn menu **Routes** bên trái. Nhấn **Create**.
2. Chọn phương thức là **GET**, đường dẫn nhập: `/get-upload-url` -> Nhấn **Create**.
3. Lặp lại tương tự để tạo thêm 2 Route nữa:
   * Phương thức **GET**, đường dẫn: `/get-history`
   * Phương thức **GET**, đường dẫn: `/get-download-url`

**Bước 2: Gắn bảo mật và kết nối Lambda**
1. Nhấn vào Route **`GET /get-upload-url`** vừa tạo.
2. Ở mục **Authorization** bên phải, nhấn **Attach authorization**. Chọn `CognitoAuth` (đã tạo ở phần trước) và nhấn **Attach**.
3. Ở mục **Integration** bên phải, nhấn **Attach integration** -> Chọn **Create and attach an integration**.
   * Integration type: Chọn **Lambda function**.
   * Integration details: Chọn hàm **`GenerateUploadUrl`**.
   * Nhấn **Create**.

**Bước 3: Lặp lại thao tác cho 2 Route còn lại**
* Với **`GET /get-history`**: Gắn bảo mật `CognitoAuth` và kết nối tới hàm Lambda **`GetUserHistory`**.
* Với **`GET /get-download-url`**: Gắn bảo mật `CognitoAuth` và kết nối tới hàm Lambda **`GenerateDownloadUrl`**.

*(Tuyệt đối không kết nối hàm `HamXuLyAnh` vào đây).*

![Kết nối Route với lớp bảo mật và Backend](/Workshop/images/4/4.8/2.3.png)

![Kết nối Route với lớp bảo mật và Backend](/Workshop/images/4/4.8/2.4.png)
