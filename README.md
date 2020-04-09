# Infrastructure SetUp

## VPC
1. Three Public Subnets in different availability zones in the same region
2. Internet Gateway with AttachInternetGateway resource
3. A public routetable which has the above 3 subnets associated with it
4. A public route in the above route table with destination CIDR block of 0.0.0.0/0 and internet gateway attached
5. Included CI/CD for automated code deployment
6. Created policies required for the roles
7. Created SSL certificate for dev in aws dev account and for prod imported SSL certificate from Namecheap account

## Cloud Formation Template
Cloudformation Template networking.json builds the network stack
Provide Parameters through CLI 

## Create Stack
Commands to execute:
aws cloudformation create-stack \
  --stack-name ${stack-name} \
  --parameters ParameterKey=Key1,ParameterValue=Value1 \
  --profile ${profile}
  --template-body file://awscertificatemanager.json

## Delete Stack
aws cloudformation delete-stack --stack-name ${stack-name} 

## Steps to import namecheap SSL certificate to aws prod account
1. Navigate to folder where SSL certificate has been downloaded.
2. Run commands as follows : openssl x509 -in ${your_ca_bundle_name}.ca-bundle -out ${your_certificate}.pem
3. openssl x509 -in ${your_crt_file_name}.crt -out ${your_domain_certificate}.pem
4. vi ${new_key}.key
5. Enter private key and save
6. aws acm import-certificate --certificate fileb://${your_domain_certificate}.pem --private-key fileb://${new_key}.key  --certificate-chain fileb://${your_certificate}.pem --profile ${profile}
