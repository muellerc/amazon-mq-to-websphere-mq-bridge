# Step 1: Set-up the on-premises broker

In this step you will create the Docker image for the IBM® MQ broker we are using to simulate the on-premises broker.

### 1. Checkout the 'mq-container' GitHub project.

> It's required to have Git installed and configured on yout machine.

Clone the 'mq-container' GitHub project by running the following comand:

``` bash
git clone git@github.com:ibm-messaging/mq-container.git
```

### 2. Build the Docker image for IBM® MQ 9.0.5.

In this step, we are creating the Docker image, by running the following commands:

``` bash
cd mq-container

git checkout 9.0.5

make build-devserver
```

### 3. Tag the Docker image and upload it to Amazon ECR.

Now we are tagging the locally created Docker image and pushing it to your ECR repository:

``` bash
$(aws ecr get-login --no-include-email --region <region>)

aws ecr create-repository \
    --repository-name amazon-mq-to-websphere-mq-bridge/mqadvanced-server-dev

docker tag  mqadvanced-server-dev:9.0.5.0-x86_64-ubuntu-16.04 <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/mqadvanced-server-dev:9.0.5

docker push <account-id>.dkr.ecr.<region>.amazonaws.com/amazon-mq-to-websphere-mq-bridge/mqadvanced-server-dev:9.0.5
```

### 4. Run und test it locally.

``` bash
docker run -it --rm -e LICENSE=accept -e MQ_QMGR_NAME=QMGR -p 9443:9443 -p 1414:1414 mqadvanced-server-dev:9.0.5.0-x86_64-ubuntu-16.04
```

To access the service, go to:  
https://127.0.0.1:9443/ibmmq/console/

> Because the MQ Console is using a self-signed certificate, it's required to accept connections to an URL which look insecure.

![Amazon MQ workshop Lab 1 step 2](/images/security_exception.png)

To log in to the IBM Console, you have to use the following default credentials (you can find all default credentials and a description, how to change it, [here](https://github.com/ibm-messaging/mq-container/blob/master/docs/developer-config.md)):  
* **User**: admin  
* **Password**: passw0rd  

After a successful login, you should see a screen similar to this one:  

![Amazon MQ workshop Lab 1 step 2](/images/IBM_Console.png)


# Completion

Congratulations, you've successfully completed step 1! You can move on to [Step 2: Set-up the JMS bridge sample service](/labs/lab-2.md)

[Return the the sample landing page](/README.md)