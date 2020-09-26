---

Copyright:
  years: 2020
lastupdated: "2020-09-25"

keywords: messages, backups, 

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Backups with {{site.data.keyword.messages-for-rabbitmq}} 
{: #backups-for-rabbitmq}

The {{site.data.keyword.messages-for-rabbitmq_full}} backups do not contain the actual messages. Your {{site.data.keyword.messages-for-rabbitmq}} deployment backups contain *only* configuration data.  

For more information on backing up your {{site.data.keyword.messages-for-rabbitmq}} service configurations, see the [Managing backups](/docs/messages-for-rabbitmq?topic=cloud-databases-dashboard-backups) section of the {{site.data.keyword.cloud}} documentation. 

Review the [management responsibilities and terms and conditions](/docs/messages-for-rabbitmq?topic=cloud-databases-responsibilities-cloud-databases) that you have when you use {{site.data.keyword.messages-for-rabbitmq}} service.


## Concepts and suggestions 

The expected operation for a {{site.data.keyword.messages-for-rabbitmq}} deployment is to keep queues short: messages are written and read in a short cycle with focus on throughput. {{site.data.keyword.messages-for-rabbitmq}} deployments are not intended as a data store like other {{site.data.keyword.cloud}} offerings. 

For message delivery with durability and consistent quality of service, you must use [quorum queues](/docs/messages-for-rabbitmq?topic=cloud-databases-high-availability#quorum-queues). 

The [Shovel plug-in](https://www.rabbitmq.com/shovel.html) can also help move messages across instances. While not a backup mechanism, this plug-in can aid in message retention. 

Remember, messages are not part of the {{site.data.keyword.messages-for-rabbitmq}} deployment backups regardless of the queue types or plug-ins implemented. 

More information on {{site.data.keyword.cloud}} can be found in the [high availability and disaster recovery](/docs/messages-for-rabbitmq?topic=cloud-databases-ha-dr) section. 


