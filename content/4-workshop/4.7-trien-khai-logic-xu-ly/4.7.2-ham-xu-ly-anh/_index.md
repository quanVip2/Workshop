---
title: "2. Image Processing & AI Function (HamXuLyAnh)"
weight: 2
pre: " <b> 4.7.2 </b> "
---

## Objectives
Build a background worker function that automatically triggers when a new image arrives in the S3 Input bucket, performs image compression, calls AI for analysis, and saves metadata.

## Permission Requirements (IAM Role)
This function must be attached with the **`AmazonRekognitionReadOnlyAccess`** policy in its IAM Role to have permissions to call the Artificial Intelligence service.

## Detailed Source Code
1. Create a Lambda function named `HamXuLyAnh` (Python 3.12). Configure the Timeout to **15 seconds** and RAM to **512MB** (to accommodate the Pillow library).
2. Paste the following code into the **Code** tab and click **Deploy**:

![AI-integrated image processing source code.](/Workshop/images/4/4.7/2.3.png)

```python
import json
import urllib.parse
import boto3
from datetime import datetime
from io import BytesIO
from PIL import Image

s3 = boto3.client('s3')
dynamodb = boto3.resource('dynamodb')
rekognition = boto3.client('rekognition') # Initialize AI Rekognition service

def lambda_handler(event, context):
    source_bucket = event['Records'][0]['s3']['bucket']['name']
    file_key = urllib.parse.unquote_plus(event['Records'][0]['s3']['object']['key'], encoding='utf-8')
    destination_bucket = 'kho-anh-nho-cua-toi-1'
    table = dynamodb.Table('ThongTinAnh')
    
    try:
        # 1. Read original image from S3
        response = s3.get_object(Bucket=source_bucket, Key=file_key)
        image_content = response['Body'].read()
        original_size = len(image_content)
        
        # 2. Graphics processing with Pillow (PIL)
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
        
        # 3. Upload compressed image to S3 Output
        s3.put_object(
            Bucket=destination_bucket, 
            Key=new_file_key, 
            Body=buffer, 
            ContentType='image/jpeg'
        )
        
        # 4. Call Amazon Rekognition for AI analysis
        buffer.seek(0)
        rek_response = rekognition.detect_labels(
            Image={'Bytes': buffer.read()},
            MaxLabels=5,
            MinConfidence=75
        )
        ai_labels = [label['Name'] for label in rek_response['Labels']]
        tags_string = ", ".join(ai_labels) if ai_labels else "Unrecognized"

        # 5. Write parameters to DynamoDB for statistics dashboard
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
        
        return {'statusCode': 200, 'body': json.dumps('Image compression and AI analysis successful!')}
    except Exception as e:
        print("System error: ", e)
        raise e