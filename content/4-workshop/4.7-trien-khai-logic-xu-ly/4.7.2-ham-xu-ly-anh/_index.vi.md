---
title: "2. Hàm Xử lý ảnh & AI (HamXuLyAnh)"
weight: 2
pre: " <b> 4.7.2 </b> "
---

## Mục tiêu
Xây dựng hàm xử lý ngầm (Background Worker) tự động kích hoạt khi có ảnh mới trong S3 Input, thực hiện nén ảnh, gọi AI phân tích và lưu metadata.

## Yêu cầu về quyền (IAM Role)
Hàm này bắt buộc phải được gắn chính sách **`AmazonRekognitionReadOnlyAccess`** trong phần IAM Role để có quyền gọi dịch vụ Trí tuệ nhân tạo.

## Mã nguồn chi tiết
1. Tạo hàm Lambda tên `HamXuLyAnh` (Python 3.12). Cấu hình Timeout lên **15 giây** và RAM **512MB** (để chứa thư viện Pillow).
2. Dán đoạn mã sau vào tab **Code** và nhấn **Deploy**:

![Mã nguồn xử lý ảnh tích hợp AI.](/Workshop/images/4/4.7/2.3.png)


```python
import json
import urllib.parse
import boto3
from datetime import datetime
from io import BytesIO
from PIL import Image

s3 = boto3.client('s3')
dynamodb = boto3.resource('dynamodb')
rekognition = boto3.client('rekognition') # Khởi tạo dịch vụ AI Rekognition

def lambda_handler(event, context):
    source_bucket = event['Records'][0]['s3']['bucket']['name']
    file_key = urllib.parse.unquote_plus(event['Records'][0]['s3']['object']['key'], encoding='utf-8')
    destination_bucket = 'kho-anh-nho-cua-toi-1'
    table = dynamodb.Table('ThongTinAnh')
    
    try:
        # 1. Đọc ảnh gốc từ S3
        response = s3.get_object(Bucket=source_bucket, Key=file_key)
        image_content = response['Body'].read()
        original_size = len(image_content)
        
        # 2. Xử lý đồ họa bằng Pillow (PIL)
        img = Image.open(BytesIO(image_content))
        if img.mode != 'RGB':
            img = img.convert('RGB')
        img.thumbnail((800, 800))
        
        buffer = BytesIO()
        img.save(buffer, format="JPEG", optimize=True, quality=50)
        buffer.seek(0)
        compressed_size = buffer.getbuffer().nbytes
        
        if '.' in file_key:
            name_without_ext = file_key.rsplit('.', 1)[0]
        else:
            name_without_ext = file_key
        new_file_key = f"resized_{name_without_ext}.jpg"
        
        user_email = "unknown"
        if "---" in file_key:
            user_email = file_key.split("---")[0]
        
        # 3. Đẩy ảnh đã nén lên S3 Output
        s3.put_object(
            Bucket=destination_bucket, 
            Key=new_file_key, 
            Body=buffer, 
            ContentType='image/jpeg'
        )
        
        # 4. Gọi Amazon Rekognition phân tích AI
        buffer.seek(0)
        rek_response = rekognition.detect_labels(
            Image={'Bytes': buffer.read()},
            MaxLabels=5,
            MinConfidence=75
        )
        ai_labels = [label['Name'] for label in rek_response['Labels']]
        tags_string = ", ".join(ai_labels) if ai_labels else "Không nhận diện được"

        # 5. Ghi thông số vào DynamoDB phục vụ Dashboard thống kê
        table.put_item(
            Item={
                'TenHinhAnh': new_file_key,
                'KichThuocGoc': original_size,
                'KichThuocNen': compressed_size,
                'KichThuoc': f"{compressed_size} bytes",
                'ThoiGianXuly': str(datetime.now()),
                'NguoiSoHuu': user_email,
                'NhanDanAI': tags_string
            }
        )
        
        return {'statusCode': 200, 'body': json.dumps('Nén ảnh và phân tích AI thành công!')}
    except Exception as e:
        print("Lỗi hệ thống: ", e)
        raise e