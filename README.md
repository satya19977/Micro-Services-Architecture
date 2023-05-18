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







## Lambda





## DynamoDB
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/dfb8c4bc-271e-47e9-8c85-0c5f6de32d1b)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/bead6ac5-dcbd-489b-8b77-7bbddc345375)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/899dea44-3d49-4380-a3f2-1ee9e2a6246d)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/1f74a67d-e125-4d13-a0b1-2d7bce2244e0)


## API
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/daa133ae-a3e1-4bb5-a07a-0645e51faf07)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/5758bf61-5459-4586-8595-b8456d43c261)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/95699313-05c1-45b1-b419-fd5ab7d58d4c)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/81be1a16-56c5-4ba9-b4a6-ee4e4a2f6129)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/4eadfcf7-6ac1-40bc-b9a3-e7d4369d3eda)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/c0fcb767-fd64-4ee2-b748-b533b61e94a5)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/ddba6d6c-b7e9-4332-9b82-1589e4cc9a26)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/a43c4798-5506-4380-9325-64a420620f29)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/bb55a0f7-98b1-4877-8f30-871f87341410)


## CleanUp
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/b10ba9c3-7c63-413b-92c3-4b828dc603e3)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/d78f21da-4392-4366-9423-2061c2380811)
![image](https://github.com/satya19977/Micro-Service-Architecture/assets/108000447/71492591-afe8-42ef-a5af-8d64372613a6)
## Conclusion
In a nutshell, these are the tools involved in the processs and following are the challenges that I faced.


[Google](https://www.google.com/)
