---
title: "4. Hàm Cấp quyền Download (GenerateDownloadUrl)"
weight: 4
pre: " <b> 4.7.4 </b> "
---

## Mục tiêu
Tạo hàm Lambda sinh ra đường dẫn tải/xem ảnh an toàn từ S3 Output Bucket khi người dùng bấm nút "Xem" trên bảng lịch sử giao diện.

## Các bước thực hiện
1. Tạo hàm Lambda tên `GenerateDownloadUrl` (Python 3.12).
2. Dán đoạn mã sau vào tab **Code** và nhấn **Deploy**:

![Cấp phát Presigned URL xem ảnh an toàn](/Workshop/images/4/4.7/2.5.png)


```python
import json
import boto3
import os

s3_client = boto3.client('s3')
OUTPUT_BUCKET_NAME = 'kho-anh-nho-cua-toi-1' 

def lambda_handler(event, context):
    try:
        file_name = event.get('queryStringParameters', {}).get('fileName')
        if not file_name:
            return {'statusCode': 400, 'body': json.dumps('Thiếu tham số fileName')}

        # Đảm bảo định dạng file chuẩn xác
        if file_name.startswith('resized_'):
            output_file_name = file_name
        else:
            name_without_ext = os.path.splitext(file_name)[0]
            output_file_name = f"resized_{name_without_ext}.jpg"

        # Tạo Presigned URL xem ảnh trong 5 phút
        presigned_url = s3_client.generate_presigned_url(
            'get_object',
            Params={'Bucket': OUTPUT_BUCKET_NAME, 'Key': output_file_name},
            ExpiresIn=300
        )
        
        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': '*'},
            'body': json.dumps({'downloadURL': presigned_url})
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'error': str(e)})}