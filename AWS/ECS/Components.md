#### [Back](./README.md)

# ECS Terminology and Components

1. **Capacity** The infra where containers run.
    * EC2 Instances
    * Fargate (Serverless)
    * ON Premises VM or Servers

2. **Controller** Deploy and manage your application that run on the container.
    * ECS Scheduler is the tool to manage the application.

3. **Provisioning** Tools to use to interface with the scheduler to deploy and manage apps and containers. Provisioning can be done via
    * AWS Management Console
    * AWS CLI
    * AWS SDK
    * Copilot
    * AWS CDK