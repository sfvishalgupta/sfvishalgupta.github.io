#### [Back](./README.md)

# Disaster Recovery in AWS

## RTO
is the longest delay the business can tolerate between the disaster event and continuation of services.

## RPO
is the longest time that may pass since the last backup window. For example, if the organization backs up files once per hour, at most the organization can lose one hour of data, the RPO is 60 minutes.

#
Amazon Web Services (AWS) lets you set up disaster recovery, both for on-premise services, and for workloads deployed in the Amazon cloud.

AWS offers four main disaster recovery (DR) strategies you can leverage to create backups and replicas that are available during disaster events. Each strategy has progressively higher cost and complexity, but lower recovery times:

1. **Backup and Restore** - involves backing up your systems and restoring them from backup in case of disaster.

2. **Pilot Light** - involves running core services in standby mode, and triggering additional services as needed in case of disaster.

3. **Warm standby** - involves running a full backup system in standby mode, with live data replicated from the production environment.

4. **Multi-site active/active** - running a full, secondary production system, ready to serve traffic when needed.




#
* **Backup & restore** provides the lowest cost, but the longest RTO
* **Pilot light** provides a medium cost and RTO
* **Warm standby** provides a high cost and low RTO
* **Multi-site active/active** provides the highest cost and a near-zero RTO