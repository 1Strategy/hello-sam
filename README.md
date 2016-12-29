# 1Strategy AWS Serverless Application Model demo

This is a sample AWS SAM CloudFormation template and Python Lambda function.

## Validate

```
aws cloudformation validate-template --template-body file://hello-sam.yaml
```

If the validate command is successful, you will get output like this:

```json
{
    "Description": "A starter AWS Lambda function.",
    "Parameters": []
}
```

## Package and Deploy

The `package` command will zip up the directory specified in the `CodeUri` property
and upload it to the specified S3 bucket/prefix.

The `package` command outputs a .yaml file suitable for use with the `cloudformation deploy`
command.

```
aws cloudformation package --template-file ./hello-sam.yaml --output-template-file output.yaml --s3-bucket my-s3-bucket --s3-prefix hello-sam
```

Run this command to deploy the CloudFormation stack. You must first use the `package` command to prepare the Lambda .zip package.

```
aws cloudformation deploy --capabilities CAPABILITY_IAM --template-file ./output.yaml --stack-name hello-sam
```


## Delete

```
aws cloudformation delete-stack --stack-name hello-sam
```
