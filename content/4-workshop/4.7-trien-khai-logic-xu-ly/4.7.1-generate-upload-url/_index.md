---
title: "1. Upload Authorization Function (GenerateUploadUrl)"
weight: 1
pre: " <b> 4.7.1 </b> "
---

## Objectives
Create a Lambda function responsible for generating a `PUT` method Presigned URL so that the web browser can push files directly to the S3 Input Bucket without exposing security keys.

## Implementation Steps
1. Create a new Lambda function named `GenerateUploadUrl` (Python 3.12).
2. In the **Code** tab, paste the following code and click **Deploy**:

![Presigned URL generation code for upload.](/Workshop/images/4/4.7/2.2.png)

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