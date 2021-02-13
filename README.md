# AWS Code Deploy Full Pipeline With Cloudformation Only - Website Example

This example extends the 
[official AWS Tutorial on using cloud formation with s3 for automatic deployments](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-cloudformation-s3.html). Instead of creating the instance, roles, security groups and installing the codedeploy agent yourself use cloudformation for everything.


Using cloudformation to do all the hard lifting:
- Setting up EC2 instance for code deploy with code deploy agent installed
- Setting up codedploy application and pipelint
- Events for automatic run of codedeploy pipeline

**You will be charged for creating AWS resources.**

## Manual
Just run the following 4 commands:

You only have to have an ec2 keypair for the instace, you have to specify the name of the keypair in the first command by replacing *\<Ec2KeyName\>* with the actual name and without \<\>.

1. `aws cloudformation create-stack --stack-name deployment-infra --template-body file://deployment-infra.yml --parameters "ParameterKey=KeyName,ParameterValue=<Ec2KeyName>" --capabilities CAPABILITY_IAM`

2. `aws cloudformation create-stack --stack-name deployment-group --template-body file://deployment-group.yml --capabilities CAPABILITY_NAMED_IAM`

3. `aws cloudformation create-stack --stack-name codepipeline-s3-events-yaml --template-body file://codepipeline-s3-events-yaml.yml --capabilities CAPABILITY_IAM`

4. `aws cloudformation create-stack --stack-name codepipeline-s3-cloudtrail-yaml --template-body file://codepipeline-s3-cloudtrail-yaml.yml`

Now simply download the demo application [SampleApp_Linux.zip](https://docs.aws.amazon.com/codepipeline/latest/userguide/samples/) SampleApp_Linux.zip and upload it to the root of your  `codepipeline-s3-events-yaml-sourcebucket-xxx` source bucket. The deployment will start automatically and you can browse the example webpage under `http://<public_instance_ip>`-

## References
- https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-cloudformation-s3.html
