---
title: "4. Download Authorization Function (GenerateDownloadUrl)"
weight: 4
pre: " <b> 4.7.4 </b> "
---

## Objectives
Create a Lambda function that generates a secure link to download/view images from the S3 Output Bucket when the user clicks the "View" button on the UI history table.

## Implementation Steps
1. Create a Lambda function named `GenerateDownloadUrl` (Python 3.12).
2. Paste the following code into the **Code** tab and click **Deploy**:

![Secure Presigned URL generation for viewing images](/Workshop/images/4/4.7/2.5.png)

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
            return {'statusCode': 400, 'body': json.dumps('Missing fileName parameter')}

        # Ensure accurate file naming format
        if file_name.startswith('resized_'):
            output_file_name = file_name
        else:
            name_without_ext = os.path.splitext(file_name)[0]
            output_file_name = f"resized_{name_without_ext}.jpg"

        # Generate Presigned URL to view image for 5 minutes
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