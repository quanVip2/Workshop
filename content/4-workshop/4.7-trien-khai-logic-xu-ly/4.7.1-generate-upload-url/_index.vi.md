---
title: "1. Hàm Cấp quyền Upload (GenerateUploadUrl)"
weight: 1
pre: " <b> 4.7.1 </b> "
---

## Mục tiêu
Tạo hàm Lambda có nhiệm vụ sinh ra một đường dẫn ký trước (Presigned URL) phương thức `PUT` để trình duyệt web có thể đẩy file trực tiếp lên S3 Input Bucket mà không cần lộ khóa bảo mật.

## Các bước thực hiện
1. Tạo một hàm Lambda mới tên là `GenerateUploadUrl` (Python 3.12).
2. Tại tab **Code**, dán đoạn mã sau vào và nhấn **Deploy**:

![Mã nguồn hàm cấp phát Presigned URL upload.](/Workshop/images/4/4.7/2.2.png)


```python
import json
import boto3
import uuid
import os

s3_client = boto3.client('s3')
BUCKET_NAME = 'kho-anh-goc-cua-toi-1'

def lambda_handler(event, context):
    try:
        query_params = event.get('queryStringParameters') or {}
        file_name = query_params.get('fileName', 'image.jpg')
        user_email = query_params.get('userEmail', 'unknown')
        
        unique_file_name = f"{user_email}---{uuid.uuid4()}---{file_name}"
        
        presigned_url = s3_client.generate_presigned_url(
            'put_object',
            Params={'Bucket': BUCKET_NAME, 'Key': unique_file_name},
            ExpiresIn=300
        )
        
        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': '*'},
            'body': json.dumps({'uploadURL': presigned_url, 'fileName': unique_file_name})
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'error': str(e)})}

