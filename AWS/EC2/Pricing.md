#### [Back](./README.md)

# AWS EC2 Pricing

1. **On Demand**
    With On-Demand Instances, you pay for compute capacity by the hour or the second, depending on which instances you run. No longer-term commitments or upfront payments are needed. You can increase or decrease your compute capacity depending on the demands of your application, and you only pay the specified hourly rates for the instance that you use.

    We recommend On-Demand Instances for the following situations:

    Users that prefer the low cost and flexibility of Amazon EC2 without any up-front payment or long-term commitment
    
    Applications with short-term, spiky, or unpredictable workloads that cannot be interrupted
    
    Applications being developed or tested on Amazon EC2 for the first time

2. **Spot**
    With Amazon EC2 Spot Instances, you can request spare Amazon EC2 computing capacity for up to 90 percent off the On-Demand price.

    We recommend Spot Instances for the following situations:
    * Applications that have flexible start and end times and can tolerate interruptions
    * Applications that you want to run or test only when the compute prices are in your price range
    * Applications that are a lower priority in your environment
    * Users with urgent computing needs for large amounts of additional capacity at a price they determine

3. **Savings Plan**
    Savings Plans is a flexible pricing model offering lower prices compared to On-Demand pricing, in exchange for a specific usage commitment (measured in USD per hour) for a 1– or 3–year period. Savings Plans offers the flexibility to evolve your usage and continue to save money. For example, if you have a Compute Savings Plan, lower prices will apply automatically when you take advantage of new instance types.

    AWS offers three types of Savings Plans:
    * Compute Savings Plans apply to usage across Amazon EC2, AWS Lambda, and AWS Fargate.
    * EC2 Instance Savings Plans apply to Amazon EC2 usage.
    * Amazon SageMaker Savings Plans apply to SageMaker usage. 

4. **Reserved Instances**
    Amazon EC2 Reserved Instances, sometimes referred to as RIs, provide a significant discount (up to 72 percent) compared to On-Demand pricing and provide a capacity reservation when used in a specific Availability Zone. Reserved Instances are not physical instances, but rather a billing discount applied to the use of On-Demand Instances in your account. 

    There are two types of Reserved Instances to choose from:

    **Standard:** These provide the most significant discount (up to 72 percent off On Demand) and are best suited for steady-state usage.

    **Convertible:** These provide a discount (up to 54 percent off On Demand) and the capability to change instance families, operating system types, and tenancies while benefitting from Reserved Instance pricing when you use the Convertible type. As with the Standard type, Convertible Reserved Instances are best suited for steady-state usage.
    
    We recommend Reserved Instances for the following situations:

    * Steady-state loads and long running systems
    * Core components with minimal high peaks or valleys of usage

5. **Dedicated Host**
    A Dedicated Host is a physical Amazon EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by permitting you to use your existing server-bound software licenses, including Windows Server, Microsoft SQL Server, and SUSE Linux Enterprise Server (subject to your license terms) and can also help you meet compliance requirements. 

    **Dedicated Hosts can be purchased in two ways:**
    * On Demand (hourly)
    * As a Reservation, for up to 70 percent off the On-Demand price
    
    We recommend Dedicated Hosts for the following situations:
    * Workloads that require server-bound software licenses
    * Security and regulatory compliance cases, where your workload cannot share hardware with other tenants.