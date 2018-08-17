# Build the project
run  
`mvn clean install`  


# Build the Docker container
run  
`docker build -t sample-with-aws-ssm .`  

`docker tag sample-with-aws-ssm:latest <account-id>.dkr.ecr.<region>.amazonaws.com/sample-with-aws-ssm:latest`  


# Upload the Docker container to Amazon ECR 
run  
`$(aws ecr get-login --no-include-email --region eu-central-1)`  
`docker push <account-id>.dkr.ecr.<region>.amazonaws.com/sample-with-aws-ssm:latest`  

# Set the env variables we have to pass to Docker, if you run it locally
`AWS_ACCESS_KEY_ID=$(aws --profile default configure get aws_access_key_id)`
`AWS_SECRET_ACCESS_KEY=$(aws --profile default configure get aws_secret_access_key)`
`AWS_REGION=$(aws --profile default configure get region)`

# Run your Docker container locally with your AWS credentials and env variables provided
for each plain-java application run  

`docker run -it --rm -e AWS_REGION=$AWS_REGION -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY sample-with-aws-ssm` .