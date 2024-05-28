#### [Back](../README.md)

# Landing Zone Accelerator (LZA)

The Landing Zone Accelerator on AWS solution deploys a foundational set of capabilities that is designed to align with AWS best practices and multiple global compliance frameworks. With this AWS Solution, you can better manage and govern your multi-account environment that have highly-regulated workloads and complex compliance requirements. When used in coordination with other AWS services, it provides a comprehensive, low-code solution across more than 35 AWS services.

Landing Zone Accelerator is provided as an open-source project that is built using the AWS Cloud Development Kit (CDK). You install directly into your environment to get full access to the infrastructure as code (IaC) solution. Through a simplified set of configuration files, you are able to configure additional functionality, controls and security services (eg. AWS Managed Config Rules, and AWS Security Hub), manage your foundational networking topology (eg. VPCs, Transit Gateways, and Network Firewall), and generate additional workload accounts using the AWS Control Tower Account Factory.

There are no additional charges or upfront commitments required to use Landing Zone Accelerator on AWS. You pay only for AWS services enabled in order to set up your platform and operate your controls. 

## Services
* ### [Global Services](./GlobalServices.md)
* ### [Identity and IAM Services](./IdentityAndIAMServices.md)
* ### [Network Services](./NetworkServices.md)
* ### [Security Services](./SecurityServices.md)
* ### [Customization Services](./CustomizationServices.md)

## Centralize Logging
The Landing Zone Accelerator Centralized Logging solution provides the ability to consolidate and manage log files from various sources into a Centralized Logging Account. This enables users to consolidate logs such as audit logs for access, configuration changes, and billing events. You can also collect Amazon CloudWatch Logs from multiple accounts and AWS Regions. The following sections discuss the types of logs that are centralized and the mechanisms used by the accelerator to centralize them.

* ### [Supported Log Types](./SupportedLogTypes.md)
* ### [Log Centralization Methods](./LogCentralizaionMethods.md)
