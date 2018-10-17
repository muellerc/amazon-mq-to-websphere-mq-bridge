# Step 3: Deploy this sample via AWS CloudFormation

In this step you will deply the entire sample via [AWS CloudFormation](https://aws.amazon.com/cloudformation/).

### 1. Select your region and launch the AWS CloudFormation template.

> To be able to run this step, it's required to have the [AWS CLI](https://aws.amazon.com/cli/) installed!.

Run the first command to launch the AWS CloudFormation template. The second command will wait, until the AWS CloudFormation stack was launched successfuly and ready to use:

TODO: in progress to develop the CloudFormation template.

```bash
aws cloudformation create-stack \
    --stack-name amazon-mq-to-websphere-mq-bridge \
    --template-body file://master.yaml \
    --capabilities CAPABILITY_IAM \
    --parameters ParameterKey=Key,ParameterValue=Value

aws cloudformation wait stack-create-complete \
    --stack-name amazon-mq-to-websphere-mq-bridge
```

### 2. Login to the IBM Console.

TODO

### 3. Login to the Amazon MQ Console / Active MQ Console.

TODO

### 4. Ingest messages on the IBM® MQ site and listen on the Amazon MQ Console.

TODO

### 5. Ingest messages on the Amazon MQ site and listen on the IBM® MQ.

TODO

# Completion

Congratulations, you've successfully completed step 3! This is the last step in the workshop.

[Return the the sample landing page](/README.md)