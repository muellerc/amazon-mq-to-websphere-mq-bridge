# Step 2: Set-up the JMS bridge sample service

In this step you will compile, package and dockerize the JMS bridge samples, we have prepared for you.

### 1. Compile the samples

> To be able to run this step, it's required to have Java 8 (or later) and Apache Maven installed!

In the root directory of this project, run the following command to compile and package the provides samples which are:  

* **1. sample-with-env-variables** - The most basic sample which is using environment variables to supply configuration parameters to the JMS bridge.

* **2. sample-with-aws-ssm** - In this sample we are using the [AWS Systems Manager Parameter Store](https://aws.amazon.com/systems-manager/features/#Parameter_Store) to store the secrets in a secure manner. The JMS bridge sample application does an secure lookup to retrive the required parameters at startup time.

* **3. sample-with-native-mapping** - This sample is demonstrating, how to map native IBM® MQ attributes. This is for example necessary, if your current solutions is using the native IBM protocoll to interact with IBM® MQ and not the JMS API. 

``` bash
mvn clean package
```

After a successful run, you should see a console output like this:
``` bash
[INFO] Reactor Summary:
[INFO]
[INFO] amazon-mq-to-websphere-mq-bridge 1.0.0-SNAPSHOT .... SUCCESS [  0.300 s]
[INFO] sample-with-env-variables .......................... SUCCESS [  9.666 s]
[INFO] sample-with-aws-ssm ................................ SUCCESS [  6.101 s]
[INFO] sample-with-nativemq-mapping 1.0.0-SNAPSHOT ........ SUCCESS [  4.572 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

### 2. Create the Amazon ECR repository which will host our Docker images

> To be able to run this step, it's required to have the [AWS CLI](https://aws.amazon.com/cli/) installed! If you haven't it installed yet, you can also use the [Amazon ECR console](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html) to create the repository.

``` bash
aws ecr create-repository \
    --repository-name amazon-mq-to-websphere-mq-bridge/sample-with-env-variables

aws ecr create-repository \
    --repository-name amazon-mq-to-websphere-mq-bridge/sample-with-aws-ssm

aws ecr create-repository \
    --repository-name amazon-mq-to-websphere-mq-bridge/sample-with-nativemq-mapping
```

### 3. Create the Docker images and upload it to Amazon ECR

> To be able to run this step, it's required to have Docker installed on your machine!.

Before you can run the following commands, please replace '\<account-id>' and '\<region>' with your values.

``` bash
$(aws ecr get-login --no-include-email --region <region>)

# first sample

docker build -t amazon-mq-to-websphere-mq-bridge/sample-with-env-variables sample-with-env-variables/.

docker tag amazon-mq-to-websphere-mq-bridge/sample-with-env-variables:latest <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-env-variables:latest

docker push <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-env-variables:latest

# seconds sample

docker build -t amazon-mq-to-websphere-mq-bridge/sample-with-aws-ssm sample-with-aws-ssm/.

docker tag amazon-mq-to-websphere-mq-bridge/sample-with-aws-ssm:latest <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-aws-ssm:latest

docker push <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-aws-ssm:latest

# third sample

docker build -t amazon-mq-to-websphere-mq-bridge/sample-with-nativemq-mapping sample-with-nativemq-mapping/.

docker tag amazon-mq-to-websphere-mq-bridge/sample-with-nativemq-mapping:latest <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-nativemq-mapping:latest

docker push <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/sample-with-nativemq-mapping:latest

```

# Completion

Congratulations, you've successfully completed step 2! You can move on to [Step 3: Deploy this sample via  AWS CloudFormation](/step-3.md)

[Return the the sample landing page](/README.md)