---
title: "3. History & Statistics Function (GetUserHistory)"
weight: 3
pre: " <b> 4.7.3 </b> "
---

## Objectives
Create a Lambda function to query the DynamoDB database by user email, convert numeric data types to standard JSON `Decimal`, and sort history in real-time.

## Implementation Steps
1. Create a Lambda function named `GetUserHistory` (Python 3.12).
2. Paste the following code into the **Code** tab and click **Deploy**:

![Cluster of 4 Lambda microservices in the system](/Workshop/images/4/4.7/2.4.png)

```python
import json
import decimal
import boto3
from boto3.dynamodb.conditions import Attr

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('ThongTinAnh')

class DecimalEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, decimal.Decimal):
            return int(obj) if obj % 1 == 0 else float(obj)
        return super(DecimalEncoder, self.default)(obj)

def lambda_handler(event, context):
    try:
        query_params = event.get('queryStringParameters') or {}
        user_email = query_params.get('userEmail')
        
        if not user_email:
            return {'statusCode': 400, 'headers': {'Access-Control-Allow-Origin': '*'}, 'body': json.dumps('Missing userEmail')}

        # Scan DynamoDB by owner email
        response = table.scan(FilterExpression=Attr('NguoiSoHuu').eq(user_email))
        items = response.get('Items', [])
        
        # Sort latest images to the top
        items.sort(key=lambda x: x.get('ThoiGianXuly', ''), reverse=True)

        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': '*'},
            'body': json.dumps(items, cls=DecimalEncoder)
        }
    except Exception as e:
        return {'statusCode': 500, 'headers': {'Access-Control-Allow-Origin': '*'}, 'body': json.dumps(str(e))}