#### [Back](../README.md)

# AWS EC2

* An instance is a VM.

* An instance type is the combination of virtual hardware components, such as CPU and memory, that make up the instance.

* Instance types are grouped together into instance families. Each instance family is optimized for specific types of use cases.
* Instance families have sub-families, which are grouped according to the combination of processor and storage used.

* A virtual central processing unit (vCPU) is a measure of processing ability. For most instance types, a vCPU represents one thread of the underling physical CPU core. For example, if an instance type has two CPU cores and two threads per core, it will have four vCPUs.

## [Advantage of Cloud Computing](./Advantages.md)
## [EC2 Families](./Families.md)

## [EC2 Pricing](./Pricing.md)
* **On Demand** You **pay full price**, by the second when you launch.
* **Spot Instances** This refers to **unused instance** resources that you can bid on. Your price is determined by market availability.
* **Reserved Instances** You agree to a **specific instance configuration** for a period of 1–3 years.
* **Dedicated Hosts** You get a full physical server.
* **Savings Plans** You commit to a certain **amount of usage** over a 1–3-year period.
## [Tools to Right-Sizing Instance](./Tools.md)

## Instance Sizing
AWS provides a wide range of instance sizes to meet the needs of different workloads. The following table provides a general overview of the instance sizes available for

| Instance Family   | Instance Size | VCPU      | Memory(GiB)   |
|   ------------    |   ---------   | --------- | -----------   |
| General purpose   | t4g.nano      | 2         | .5            |
| General purpose   | t4g.micro     | 2         | 1             |
| General purpose   | t4g.small     | 2         | 2             |
| General purpose   | t4g.medium    | 2         | 4             |
| General purpose   | t4g.large     | 2         | 8             |


## Instance Family Growth
AWS provides a wide range of instance sizes to meet the needs of different workloads. The following table provides a general overview of the instance sizes available for

| Instance Family   | Instance Size | VCPU      | Memory(GiB)   |
|   ------------    |   ---------   | --------- | -----------   |
| Compute optimized | c5.xlarge     | 4         | 8             |
| Compute optimized | c5.2xlarge    | 8         | 16            |
| Compute optimized | c5.4xlarge    | 16        | 32            |
| Memory optimized  | r5g.xlarge    | 4         | 32            |
| Memory optimized  | r6g.2.xlarge  | 8         | 64            |
| Memory optimized  | r6g.4.xlarge  | 16        | 128           |

