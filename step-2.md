# Step 2: Deploy the broker infrastructure via AWS CloudFormation

In this step you will deply the entire sample via [AWS CloudFormation](https://aws.amazon.com/cloudformation/).

### 1. Select your region and launch the AWS CloudFormation template.

> To be able to run this step, it's required to have the [AWS CLI](https://aws.amazon.com/cli/) installed!.

Run the first command to launch the AWS CloudFormation template. The second command will wait, until the AWS CloudFormation stack was launched successfuly and ready to use. Alternatively, you can also open your CloudFormation console and watch the resource creation process. It takes up to 15 minutes to complete:

```bash
aws cloudformation create-stack \
    --stack-name amazon-mq-to-websphere-mq-bridge-environment \
    --template-body file://master.yaml \
    --capabilities CAPABILITY_IAM

aws cloudformation wait stack-create-complete \
    --stack-name amazon-mq-to-websphere-mq-bridge-environment
```

### 2. Login to the IBM Console.

In your [Fargate console](https://console.aws.amazon.com/ecs/home?#/clusters/ibm-mq-cluster/tasks) you should see one running task with the task definition name **ibm-mq-broker-task:#**. Klick on the task link and lookup the public IP address which is assigned to your IBM MQ broker.  

To access the console of your IBM MQ broker, go to:  
https://\<public IP\>:9443/ibmmq/console/

You can use this web console to read messages from the broker and write messages to it.

### 3. Login to the Amazon MQ Console / Active MQ Console.

Open a new tab and got to your [Amazon MQ broker console](https://console.aws.amazon.com/amazon-mq/home?#/brokers/) and click on the broker with the name **AmazonMQBroker**. In the **Connections** section, figure out which of the both **ActiveMQ Web Console** links are active. To access the web console, provide the Amazon MQ broker user and password. If you don't have provided a specific value, use the following ones:  
* User: AmazonMQBrokerUserName
* Password: AmazonMQBrokerPassword

You can use this web console to read messages from the broker and write messages to it.

# Completion

Congratulations, you've successfully completed step 2! You can move on to [Step 3: Set-up the JMS bridge sample services](/labs/lab-3.md)

[Return the the sample landing page](/README.md)