---
title:  "Lambda CLI"
layout: blog
order: 0
topic: AWS
topic_path: /docs/aws/index.html
---
This guide explains how to use AWS Lambda over the CLI. The guide assumes you have already set up the AWS command line interface. You can verify proper setup using the command `aws --version`. Read the [guide published by AWS](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-awscli.html) for more information.

# Commands

Create the execution role
```bash
aws iam create-role --role-name lambda-ex --assume-role-policy-document file://roles/trust-policy.json
```

Grant Lambda execution permissions to the role
```bash
aws iam attach-role-policy --role-name lambda-ex \
--policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole
```

Delete a function
```bash
aws lambda delete-function --function-name my-function
```

Create deployment package
```bash
zip function.zip index.js
```

Create a function
```bash
aws lambda create-function --function-name my-function \
--zip-file fileb://function.zip --handler index.handler --runtime nodejs12.x \
--role arn:aws:iam::123456789012:role/lambda-ex
```

Updating a function
```bash
aws lambda update-function-code --function-name my-function --zip-file fileb://function.zip
```

List Lambda functions
```bash
aws lambda list-functions --max-items 10
```

Invoke function with logs
```bash
aws lambda invoke --function-name my-function out --log-type Tail \
--query 'LogResult' --output text |  base64 -d
```