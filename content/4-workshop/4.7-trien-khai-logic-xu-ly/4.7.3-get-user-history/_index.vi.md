---
title: "3. Hàm Lấy lịch sử & Thống kê (GetUserHistory)"
weight: 3
pre: " <b> 4.7.3 </b> "
---

## Mục tiêu
Tạo hàm Lambda truy vấn cơ sở dữ liệu DynamoDB theo email người dùng, chuyển đổi kiểu dữ liệu số `Decimal` chuẩn JSON, và sắp xếp lịch sử theo thời gian thực.

## Các bước thực hiện
1. Tạo hàm Lambda tên `GetUserHistory` (Python 3.12).
2. Dán đoạn mã sau vào tab **Code** và nhấn **Deploy**:

![Cụm 4 vi dịch vụ Lambda trong hệ thống](/Workshop/images/4/4.7/2.4.png)


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
            return {'statusCode': 400, 'headers': {'Access-Control-Allow-Origin': '*'}, 'body': json.dumps('Thiếu userEmail')}

        # Quét DynamoDB theo email sở hữu
        response = table.scan(FilterExpression=Attr('NguoiSoHuu').eq(user_email))
        items = response.get('Items', [])
        
        # Sắp xếp ảnh mới nhất lên đầu
        items.sort(key=lambda x: x.get('ThoiGianXuly', ''), reverse=True)

        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': '*'},
            'body': json.dumps(items, cls=DecimalEncoder)
        }
    except Exception as e:
        return {'statusCode': 500, 'headers': {'Access-Control-Allow-Origin': '*'}, 'body': json.dumps(str(e))}