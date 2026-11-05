# Tutorial 

- https://github.com/alexdebrie/dynamodb-instagram
- https://www.youtube.com/watch?v=Q6-qWdsa8a4
- A complete, practice-ready Amazon DynamoDB single-table design covers core NoSQL concepts: Partition Key (PK), Sort Key (SK), composite primary keys, Global/Local Secondary Indexes (GSI/LSI), and overloaded entities (Users, Orders, Products)

```python
import json
import boto3
from boto3.dynamodb.conditions import Key
from botocore.exceptions import ClientError
from pprint import pprint

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')



response = table.put_item(
    Item = {'email': 'nagu@local.com',
 'empid': '2988',
 'english': '35',
 'maths': '75',
 'science': '50',
 'telugu': '65',
 'userId': '2',
 'username': 'nagu'},
 
 ConditionExpression = Attr('userId').not_exists()
 
)

res = table.get_item(
    Key={"userId": "2"},
    ProjectionExpression="#n, #e",
    ExpressionAttributeNames={
        "#n": "username",
        "#e": "email"
    }
)

response = table.update_item(
    Key={"userId": "1"},
    UpdateExpression="SET #n = :name",
	ConditionExpression="attribute_exists(userId)",
    ExpressionAttributeNames={
        "#n": "username"
    },
    ExpressionAttributeValues={
        ":name": "Kumar"        
    },
    ReturnValues="ALL_NEW"
)

res = table.delete_item(
    Key = {"userId":"5"}
)
```
```python
UpdateExpression="DELETE skills :skill"
ExpressionAttributeValues={
    ":skill": {"Python"}
}

UpdateExpression="ADD loginCount :inc"
ExpressionAttributeValues={":inc": 1}

UpdateExpression="REMOVE city"

UpdateExpression="SET age = :age"
ExpressionAttributeValues={":age": 31}
```
