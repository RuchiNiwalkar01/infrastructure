# Infrastructure SetUp

## VPC
Three Public Subnets in different availability zones in the same region
Internet Gateway with AttachInternetGateway resource
A public routetable which has the above 3 subnets associated with it
A public route in the above route table with destination CIDR block of 0.0.0.0/0 and internet gateway attached

## Cloud Formation Template
Cloudformation Template networking.json builds the network stack
Provide Parameters through CLI 

## Create Stack
Commands to execute:
aws cloudformation create-stack \
  --stack-name csye6225demo \
  --parameters ParameterKey=InstanceTypeParameter,ParameterValue=t2.micro \
  --template-body file://networking.json

## Delete Stack
aws cloudformation delete-stack --stack-name csye6225demo
