#### [Back](./README.md)

# Disadvantages of AWS QLDB

1. QLDB currently does not support a backup or restore feature as of now. Export to S3 can be done periodically to maintain a backup. S3 lifecycle can help in archiving the old data depending on the need.

2. Amazon QLDB does not support a point-in-time restore feature as of now.

3. QLDB does not support cross-region replication. However, export to S3 and S3 buckets can be configured for cross-region replication.

4. For encryption, currently, customer-managed CMKs (Customer Master Keys) are not supported. Amazon QLDB uses AWS-owned keys to encrypt customer data.

5. Designing the database with proper index and query patterns at an earlier stage is important to avoid significant performance problems, including query latency, transaction timeouts, and concurrency conflicts in the future.