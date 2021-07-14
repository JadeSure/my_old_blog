---
layout:     post
title:      AWS Service Based Project - Music Subscription Application
subtitle:   This project utilizes EC2, DynamoDB, S3 Bucket, Flask
date:       2021-05-05
author:     Shuo Wang
header-img: img/post-bg-awslogo.jpg
catalog: true
tags:
    - ubuntu
    - AWS
    - EC2
    - Flask
---

---


## AWS DynamoDB Web Service Connection
1. signing up for AWS  
2. geting an AWS Access Key by IAM  
There are two ways to connect AWS service from backend server to AWS service by credential.    
3.1 the first way is configuring your credentials to enable authorization(by creating the credentials file or aws configure).  
3.2 use environment variables.   
```python
class DynamoDBConnection():
def __init__(self, dynamoDB = None):
    session = boto3.Session(
        aws_access_key_id=ACCESS_KEY,
        aws_secret_access_key=SECRET_KEY
    )
    if not dynamoDB:
        self.dynamoDB = session.resource('dynamodb')
```
[Setting Up DynamoDB(Web Service)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SettingUp.DynamoWebService.html)  
[boto3 tutorial + dynamodb](https://www.section.io/engineering-education/python-boto3-and-amazon-dynamodb-programming-tutorial/
)  
[boto3 API documentation & tutorial](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/dynamodb.html
)

## AWS S3 Bucket Service Connection
```python
os.environ['AWS_DEFAULT_REGION'] = 'us-east-1'

self.s3_client = boto3.client('s3', aws_access_key_id=ACCESS_KEY,
aws_secret_access_key=SECRET_KEY)

```

## Deploy Flask Application to EC2
1. pip freeze -> requirements.txt in the local machine to fix the working environment
2. pip install -r requirements.txt




## Reference
[aws code documentation](https://docs.aws.amazon.com/code-samples/latest/catalog/python-dynamodb-TryDax-01-create-table.py.html
)


