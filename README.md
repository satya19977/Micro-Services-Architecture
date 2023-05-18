# Micro-Services-Architecture
Resources Used - API Gateway , Lambda , DynamoDB, IAM

# Micro Service Architecture
![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/0c8a4655-b30e-4142-81c5-65efe33a842e)

**API gateway is used to invoke a python function running in Lambda to insert user data in DynamoDB**

## Code Snippets
DynamoDB Create Operation
```
{
    "operation": "create",
    "tableName": "lambda-apigateway",
    "payload": {
        "Item": {
            "id": "1",
            "name": "Satya"
        }
    }
}
```
IAM Permissions
```
{
"Version": "2012-10-17",
"Statement": [
{
  "Sid": "Stmt1428341300017",
  "Action": [
    "dynamodb:DeleteItem",
    "dynamodb:GetItem",
    "dynamodb:PutItem",
    "dynamodb:Query",
    "dynamodb:Scan",
    "dynamodb:UpdateItem"
  ],
  "Effect": "Allow",
  "Resource": "*"
},
{
  "Sid": "",
  "Resource": "*",
  "Action": [
    "logs:CreateLogGroup",
    "logs:CreateLogStream",
    "logs:PutLogEvents"
  ],
  "Effect": "Allow"
}
]
}
```
Lambda Code
```
from __future__ import print_function

import boto3
import json

print('Loading function')


def lambda_handler(event, context):
    '''Provide an event that contains the following keys:

      - operation: one of the operations in the operations dict below
      - tableName: required for operations that interact with DynamoDB
      - payload: a parameter to pass to the operation being performed
    '''
    #print("Received event: " + json.dumps(event, indent=2))

    operation = event['operation']

    if 'tableName' in event:
        dynamo = boto3.resource('dynamodb').Table(event['tableName'])

    operations = {
        'create': lambda x: dynamo.put_item(**x),
        'read': lambda x: dynamo.get_item(**x),
        'update': lambda x: dynamo.update_item(**x),
        'delete': lambda x: dynamo.delete_item(**x),
        'list': lambda x: dynamo.scan(**x),
        'echo': lambda x: x,
        'ping': lambda x: 'pong'
    }

    if operation in operations:
        return operations[operation](event.get('payload'))
    else:
        raise ValueError('Unrecognized operation "{}"'.format(operation))
```
Lambda Test Code
```
{
    "operation": "echo",
    "payload": {
        "somekey1": "somevalue1",
        "somekey2": "somevalue2"
    }
}
```
## IAM

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/2d0c07b4-428c-4bf5-8ca5-ffa3239226ad)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/fd439355-0ff3-4a66-a03a-9017a0070d54)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/d8e761c6-7947-446a-8c74-910ecaffab9f)


![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/c5d2554a-c55e-4be8-bf08-f1bdfb3c4d37)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/b6b0a5f3-4a43-48fb-868a-5147ec2c43a6)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/50735248-7b71-44ae-9f3d-f650c14e744d)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/8d55f080-966d-46d3-85dd-f517209401aa)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/f5a094f4-0d6e-45dc-aa5f-0b4798ebe366)


## Lambda

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/483c7028-b797-4452-9957-cc30ed92bafb)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/aeb699a4-fdb7-4a77-86b4-374e2ac3c194)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/87e59aec-11a5-41f9-b2e2-daf89f828d1f)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/165dace2-70b9-400d-8db5-dd74bc04f786)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/1b8b07d7-6d52-4439-87a8-fcd029c9d327)

## DynamoDB

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/f3246cd2-4aef-4066-b79a-2a042400a7f0)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/127c37ff-a663-4488-8dff-040a565a1ce0)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/949f1471-d579-42ef-ac9d-a7899ffa4d71)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/7de808d6-dee6-4972-9572-ff86dc0ab28f)



## API

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/81479fef-ab4b-43fa-96ae-f6755d45d7a1)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/cb8ca965-34c2-4e99-89f9-b393f8c25057)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/13540743-c3f5-4d18-8307-159d62c5b717)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/e95444c7-7da5-4700-aa75-ab654d3e00f4)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/2a7aed23-f76e-4790-8098-27302cbea62f)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/2556f7fa-e43f-456f-a420-9c47cd0a81d5)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/229f151e-e860-4cbf-9b78-6bd5204bcc50)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/6318df50-ea9c-4b0f-882f-326ee80af085)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/71d4b56c-46d0-4ffb-88be-38245f62698f)

## CleanUp

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/46847419-0731-4c10-b23c-f96b6568b59b)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/aa8fc1b6-efda-4bda-a5bb-667a62a403e7)

![image](https://github.com/satya19977/Micro-Services-Architecture/assets/108000447/c293a19f-2868-48a0-b991-b6da9c3c4ab7)



