---

Copyright:
  years: 2018, 2020
lastupdated: "2020-03-16"

keywords: rabbitmq, databases, memory alarms, disk alarms, monitoring, disk I/O

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Performance
{: #performance}

{{site.data.keyword.messages-for-rabbitmq_full}} deployments can be both manually [scaled to your usage](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-resources-scaling), or configured to [autoscale](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-autoscaling) under certain resource conditions. There are a few factors to consider if you are tuning the performance of your deployment.

## Monitoring your deployment

{{site.data.keyword.messages-for-rabbitmq}} deployments offer an integration with the [{{site.data.keyword.cloud_notm}} Monitoring service](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-sysdig-monitoring) for basic monitoring of resource usage on your deployment. Many of the available metrics, like disk usage and IOPS, are presented to help you configure [autoscaling](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-autoscaling) on your deployment. Observing trends in your usage and configuring the autoscaling to respond to them can help alleviate performance problems before your databases become unstable due to resource exhaustion.

## RabbitMQ Memory Usage

[RabbitMQ provides a robust breakdown of memory usage](https://www.rabbitmq.com/memory-use.html#breakdown), which can provide you information on how memory resources are allocated and being used in your deployment. Most notably, connections, queue mirrors, and accumulated messages all use memory. If your use-case calls for many open connections at a time, you may want to look into increasing memory. Likewise, if you have queues that only contain transient messages that don't need replication, you can bring down memory usage by adjusting their [mirroring policy](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-high-availability#high-availability-queue-configuration). Be aware that changes to mirroring policy where messages have fewer or no mirrors can cause messages to be deleted on node restarts and those messages are gone forever.

Occasionally, RabbitMQ can experience memory spikes. Specifically with {{site.data.keyword.messages-for-rabbitmq}} deployments, updates and maintenance where we restart or delete a node causes memory usage to increase in order to resync the restarted or new node. If your RabbitMQ consistently uses a high percentage of its available memory, one of these spikes can run your deployment out of memory and cause it to crash. It is a good idea to scale your memory so that it can accommodate resyncing a node.

### RabbitMQ Memory Alarms

By default, when the RabbitMQ server uses above 40% of the available RAM, it raises a memory alarm and blocks incoming messages from publishers. The memory alarm is cleared if consumers consume enough of the messages or the messages are moved to disk. Once the memory alarm is cleared normal service resumes, and the publishers are unblocked. Note that this does not prevent the RabbitMQ server from using more than 40% of the allocated memory, it is merely the point at which publishers are throttled. More information about memory alarms can be found in the [RabbitMQ documentation](https://www.rabbitmq.com/memory.html).

## RabbitMQ Disk Alarms

By default, when the RabbitMQ server detects that free disk space has dropped below a certain threshold, it raises a disk alarm. The threshold for {{site.data.keyword.messages-for-rabbitmq}} is 80% of your deployment's disk size. The alarm blocks incoming messages from publishers and prevents messages in memory from being written to disk. The alarm is cluster-wide so if disk space on one node gets to low, the alarm blocks on all nodes. To clear the alarm, either messages that have been written to disk need to be consumed and that space reclaimed, or you need to scale your deployment to a larger disk size.

More information about memory alarms can be found in the [RabbitMQ documentation](https://www.rabbitmq.com/disk-alarms.html)

## Disk IOPS

The number of Input-Output Operations per second (IOPS) is limited by the type of storage volume that is being used. Storage volumes for {{site.data.keyword.messages-for-rabbitmq}} deployments are provisioned on [Block Storage Endurance Volumes in the 10 IOPS per GB tier](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance). IOPS limits can affect RabbitMQ message throughput and storage operations, and hitting the limits can cause disk to fall behind on reclaiming space after messages are consumed, leading to disk alarms and publisher throttling until activity slows down. You can increase the number IOPS available to your deployment by increasing disk space.

## Quorum Queues

Starting in RabbitMQ 3.8, high-availability can be managed with [quorum queues](https://www.rabbitmq.com/quorum-queues.html). Using quorum queues impacts performance; it needs more memory and disk space for the WAL that it uses to maintain state for operations. It also needs more disk I/O as it persists all data on disk. If you have implemented quorum queues, or are considering them, the RabbitMQ documentation has a good write up of their affect on both [resource use](https://www.rabbitmq.com/quorum-queues.html#resource-use) and [performance](https://www.rabbitmq.com/quorum-queues.html#performance).

## RabbitMQ Alarm Monitoring

When a disk or memory alarm is triggered, RabbitMQ emits a [`connection.blocked` notification](https://www.rabbitmq.com/connection-blocked.html) to publishing connections. Many drivers support the protocol necessary to catch the notification so you can design your application to respond to RabbitMQ alarms.

You can also monitor alarms from the [RabbitMQ HTTP API](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-management-plugin#rabbitmq-management-http-api). Use the `GET /api/nodes` endpoints, and look for `mem_alarm` and `disk_free_alarm` in the response.

For additional checks related to memory alarms, you can gather information related to a single node's memory using the `GET /api/nodes/{node}/memory` endpoint.

## Standard Health Checks

The [RabbitMQ HTTP API](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-management-plugin#rabbitmq-management-http-api) provides a couple of [health check](https://www.rabbitmq.com/monitoring.html#health-checks) endpoints that allow you to verify the state of the RabbitMQ nodes in your deployment. 

- [All Nodes](https://www.rabbitmq.com/monitoring.html#node-metrics) - `GET /api/healthcheck/node`
- [Single Node](https://www.rabbitmq.com/monitoring.html#node-metrics) - `GET /api/healthcheck/node/<node_name>`

Health checks consume system resources. For smaller, less busy deployments, the health check shouldn't take very long to give you a response. Larger deployments, or deployments under load, can take some time to return results.
{: #tip}

## Notes for Compose Users

If you are migrating to {{site.data.keyword.messages-for-rabbitmq}} from an IBM Cloud Compose For RabbitMQ deployment, you might find the article [Getting Started with Messages for RabbitMQ](https://www.ibm.com/cloud/blog/getting-started-with-ibm-cloud-messages-for-rabbitmq) helpful. The configuration of alarms as well as the lack of autoscaling differs from the your previous deployments, and it does have an affect on performance. Testing and tuning your new deployment before moving over production work loads is highly recommended.