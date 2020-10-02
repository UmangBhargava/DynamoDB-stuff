Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. DynamoDB lets you offload the administrative burdens of operating and scaling a distributed database so that you don't have to worry about hardware provisioning, setup and configuration, replication, software patching, or cluster scaling. DynamoDB also offers encryption at rest, which eliminates the operational burden and complexity involved in protecting sensitive data.


This Repository is about DynamoDB Best Practices, and how to avoid Throttling on Provisioned and On Demand Tables

Each partition on a DynamoDB table is subject to a hard limit of 1,000 write capacity units and 3,000 read capacity units. If your workload is unevenly distributed across partitions, or if the workload relies on short periods of time with high usage (a burst of read or write activity), the table might be throttled.

DynamoDB adaptive capacity automatically boosts throughput capacity to high-traffic partitions. However, each partition is still subject to the hard limit. This means that adaptive capacity can't solve larger issues with your table or partition design. To avoid hot partitions and throttling, optimize your table and partition structure.

**Resolution**

Before implementing one of the following solutions, use Amazon CloudWatch Contributor Insights to find the most accessed and throttled items in your table. Then, use the solutions that best fit your use case to resolve throttling.

1) Distribute read and write operations as evenly as possible across your table.

A hot partition can degrade the overall performance of your table. For more information, see Designing Partition Keys to Distribute Your Workload Evenly.

2) Implement a caching solution. 

If your workload is mostly read access to static data, then query results can be delivered much faster if the data is in a well‑designed cache rather than in a database. DynamoDB Accelerator (DAX) is a caching service that offers fast in‑memory performance for your application. You can also use Amazon ElastiCache.

3) Implement error retries and exponential backoff. 

Exponential backoff can improve an application's reliability by using progressively longer waits between retries. If you're using an AWS SDK, this logic is built‑in. If you're not using an AWS SDK, consider manually implementing exponential backoff. For more information, see Error Retries and Exponential Backoff in AWS.

For more information, refer here[https://aws.amazon.com/premiumsupport/knowledge-center/dynamodb-table-throttled/]
