---

Copyright:
  years: 2018
lastupdated: "2018-10-15"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Architecture

{{site.data.keyword.messages-for-rabbitmq_full}} is a managed cloud database service that runs in containers that are orchestrated by Kubernetes. It is fully integrated into the {{site.data.keyword.cloud_notm}} ecosystem. The database, storage, and monitoring all run in {{site.data.keyword.cloud_notm}}.

## RabbitMQ Nodes

{{site.data.keyword.messages-for-rabbitmq}} deployments contain a cluster with three nodes. All three nodes are equal peers. The cluster is spread over the region's availability zones. If one data member becomes unreachable, your cluster continues to operate normally.

### Storage

All backup storage for {{site.data.keyword.messages-for-rabbitmq}} is on {{site.data.keyword.cloud_notm}} Object Storage.

### Full-disk Encryption

All {{site.data.keyword.messages-for-rabbitmq}} deployments have encryption at rest. Your data and backups reside on servers that have volume-level encryption enabled.

## Connections

{{site.data.keyword.messages-for-rabbitmq}} is configured to accept connections on two TCP listeners, which are placed behind a Kubernetes endpoint. This endpoint provides the connection for your applications. Having two listeners behind the endpoint allows for applications to maintain connectivity if one of the listeners becomes unreachable.

### Encryption in Transit

All {{site.data.keyword.messages-for-rabbitmq}} connections are TLS/SSL enabled and support TLS version 1.2. Self-signed certificates are provided to enable applications to validate the server upon connection. The RabbitMQ node-to-node traffic is also TLS encrypted.

## Access Management

{{site.data.keyword.messages-for-rabbitmq}} is an IAM-integrated service. Access to the service is governed by the roles and attributes that are consistent with IAM-integrated services across the {{site.data.keyword.cloud_notm}}. For more information about IAM, see the [What is IAM?](https://{DomainName}/docs/iam/index.html#iamoverview) documentation. For details on how IAM affects access to {{site.data.keyword.messages-for-rabbitmq}}, see the [Managing Access](./reference-access-management.html) page.

