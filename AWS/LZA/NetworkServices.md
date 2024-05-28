#### [Back](./README.md)

# Network Services

| Service/Feature | Resources | Details | 
| --------------- | --------- | ------- |
| Delete Default Amazon VPC             |  Default VPC | If enabled, deletes the default VPC in each account and region managed by the accelerator.
| AWS Direct Connect                    | Gateways, virtual interfaces, and gateway associations | Define Direct Connect gateways, virtual interfaces, and Direct Connect Gateway associations.
| Amazon ELB                            | Gateway Load Balancers, endpoint services, and endpoints | Define a centrally-managed Gateway Load Balancer with an associated VPC endpoint service. Define Gateway Load Balancer endpoints that consume the service, allowing for deep packet inspection of workloads.
| AWS Network Firewall                  | Network Firewalls, policies, and rule groups | Define centrally-managed firewall rule groups and policies. Define Network Firewall endpoints that consume the policies, allowing for deep packet inspection of workloads.
| Amazon Route 53 Resolver              | Resolver endpoints, rules, DNS firewall rule groups, and query logging configurations | Define centrally-managed Resolver endpoints, Resolver rules, DNS firewall rule groups, and query logging configurations. DNS firewall rule groups, Resolver rules, and query logging configurations can be associated to VPCs defined in VpcConfig / VpcTemplatesConfig.
| AWS Site-to-Site VPN                  | Customer gateways and VPN connections | Define Customer gateways and VPN connections that terminate on Transit Gateways or Virtual Private Gateways.
| AWS Transit Gateway                   | Transit Gateways and Transit Gateway route tables | Define Transit Gateways to deploy to a specified account and region in the AWS Organization.
| Amazon VPC                            | Customer-managed prefix lists | Define customer-managed prefix lists to deploy to account(s) and region(s) in the AWS Organization. Prefix lists can be referenced in place of CIDR ranges in subnet route tables, security groups, and Transit Gateway route tables.
| Amazon VPC IP Address Manager (IPAM)  | IPAM pools and scopes | Enable IPAM delegated administrator and configuration settings for IPAM pools and scopes. NOTE: IPAM is required for VPCs and subnets configured to use dynamic IPAM CIDR allocations.
| Amazon VPC Templates                  | VPCs, subnets, security groups, NACLs, route tables, NAT Gateways, and VPC endpoints | Deploys a standard-sized VPC to multiple defined account(s) and/or organizational unit(s).
