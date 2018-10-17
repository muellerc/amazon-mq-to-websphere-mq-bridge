# JMS Bridge Sample

## Overview

The [JMS Bridge Sample](http://) introduces an architecture which allows your to bridge from your existing on-premisses messaging broker (IBM® MQ in our example) to a managed message broker in the cloud ([Amazon MQ](https://aws.amazon.com/amazon-mq/) in our case).  

Quite often, these message brokers are interfaced by many applications and customers struggeling how to migrate these applications to the cloud. To reduce the risk, they don't want to migrate in a "big bang" one step szenario, but looking for an architecture which allows a step by migration to move one service after the other to the cloud.  

## Architecture

In this sample, we are setting up an environment as below. To simulate the on-premises message broker, we are running IBM® MQ in [AWS Fargate](https://aws.amazon.com/fargate/). For the managed message broker in the cloud, we are obviously using [Amazon MQ](https://aws.amazon.com/amazon-mq/). To run the JMS bridge sample to exchange messages between both message broker, we are also using [AWS Fargate](https://aws.amazon.com/fargate/) because we don't want to reduce the time as much as possible, to manage an operate the solution.

![JMS Bridge Sample architecture](/images/architecture.png)

## Go Build!

To build and run this example, you have to follow 3 steps we will discuss in detail.

* **[Step 1: Set-up the on-premises broker](/step-1.md)** - Here, we are creating a Docker image which contains the IBM® MQ broker to have an easy way to run this broker in AWS.

* **[Step 2: Set-up the JMS bridge sample service](/step-2.md)** - Here, we are creating a Docker image which includes the JMS bridge sample service to have an easy way to run this application.

* **[Step 3: Deploy this sample via AWS CloudFormation](/step-3.md)** - Here, we are executing an [AWS CloudFormation](https://aws.amazon.com/cloudformation/) template to which is provisioning our on-premises IBM® MQ in [AWS Fargate](https://aws.amazon.com/fargate/), create the managed [Amazon MQ](https://aws.amazon.com/amazon-mq/) broker and deploy our JMS bridge sample service to [AWS Fargate](https://aws.amazon.com/fargate/).