#### [Back](./README.md)

# AWS Ec2 Families

## **Below are the 5 Families**

### 1. General Purpose
* General purpose instances are designed to handle a wide variety of workloads. They are a good choice for applications that are not memory or I/O intensive

|       |       |       |       |       |       |
| ---   | ---   | ---   | ---   | ---   | ---   |
| Mac   | M1    |       |       |       |       |
| T4g   | T3    | T3a   | T2    |
| M6g   | M6gd  | M6i   | M6a   |
| M5    | M5a   | M5d   | M5n   | M5dn  | M5zn  |
| M4    | A1    |

### 2. Compute Optimized
Compute optimized instances are ideal for compute-bound applications that benefit from high-performance processors. Instances belonging to this family are well suited for compute-intensive operations, such as the following:

* Batch processing workloads
* Media transcoding
* High performance web servers
* High performance computing (HPC)
* Scientific modeling
* Dedicated gaming servers and ad server engines
* Machine learning (ML) inference 

|       |       |       |       |       |
| ---   | ---   | ---   | ---   | ---   |
| C7g   |
| C6g   | C6gn  | C6gd  | C6i   |
| C5    | C5d   | C5a   | C5ad  | C5n   |
| C4    | 


### 3. Memory Optimized
Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.

|       |       |           |           |       |       |       |
| ----- | ----- | --------- | --------- | ----- | ----- | ----- |
| R6g   | R6i   |
| R5    | R5a   | R5d       | R5ad      | R5gd  | R5b   | R5n   |
| Rdn   | R4    |
| X2gd  | X2idn | X2iedn    | X2iezn    | X1e    | X1    |
| High <br>Memory Instance |
| z1d |

### 4. Storage Optimized
Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random input/output (I/O) operations per second (IOPS) to applications.

|       |       |       |
| ----- | ----- | ----- |
| lm4gn |
| lsgen | l4i   |
| l3    | l3en  |
| l2    |
| D2    | D3    | D3en  |
| H1    |
| DB    |

### 5. Accelerated Computing
Accelerated computing instances use hardware accelerators, or co-processors, to perform some functions more efficiently than is possible in software running on CPUs. Examples of such functions include floating point number calculations, graphics processing, and data pattern matching. Accelerated computing instances facilitate more parallelism for higher throughput on compute-intensive workloads.

If you require high processing capability, you will benefit from using accelerated computing instances, which provide access to hardware-based compute accelerators such as graphics processing units (GPUs), field programmable gate arrays (FPGAs), or AWS Inferentia.

|       |       |       |       |       |
| ----- | ----- | ----- | ----- | ----- |
| P4    | P4d   | P3    | P3dn  | P2    |
| DL1   | Tm1   |
| G5    | G5g   | G4dn  | G4ad  | G3    |
| F1    | VT1   |


## Decoding instances names
Instance names are a combination of the instance family, generation, and size. They can also indicate additional capabilities, such as specific processor type or optimized networking performance.

**Example** (m5zn.xlarge)

* **m:-** Instance family, M is general purpose instance sub-family. M can be remembered as Main, Most, Many.

* **5:-** Instance Generation, with higher number being the newer generation. The newer generation often provide a performance improvement, a cost saving, or both 

* **z:-** Attribute, not all instance have attribute option, This provides additional info about the instance capability, 
In this case z represents the high frequency and tells us this instance is ideal for high single-thread performance.

* **n:-** Additional Info, n stands for n/w and indicates this instance is optimized for high throughput and low n/w latency.

* **xlarge:-** Size, The larger the size, the more resources, such as CPU and Memory, Sizes are based on the combination of h/w. 

## Additional Characteristics
* **a:-** AMD processors
* **g:-** AWS Graviton processors
* **i:-** Intel processors
* **d:-** Instance store volumes
* **n:-** Network optimization
* **b:-** Block storage optimization
* **e:-** Extra storage or memory
* **z:-** High frequency