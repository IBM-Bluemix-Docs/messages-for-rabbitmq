---
copyright:
  years: 2020
lastupdated: "2020-03-05"

keyowrds: rabbitmq, upgrading, major versions, changing versions

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Upgrading to a new Major Version
{: #upgrading}

Once a major version of a database is at its End Of Life (EOL), it is a good idea to upgrade to a current major version. 

You can find the available versions of RabbitMQ on the [{{site.data.keyword.messages-for-rabbitmq_full}} the catalog](https://cloud.ibm.com/catalog/messages-for-rabbitmq) page, from the cloud databases cli plugin command [`ibmcloud cdb deployables-show`](/docs/databases-cli-plugin?topic=cloud-databases-cli-cdb-reference#deployables-show), or from the cloud databases API [`/deployables`](https://cloud.ibm.com/apidocs/cloud-databases-api#get-all-deployable-databases) endpoint.

Upgrading is handled through [restoring a backup](/docs/messages-for-rabbitmq?topic=cloud-databases-dashboard-backups#restoring-a-backup) of your data into a new deployment running the new version. Restoring from a backup has a number of advantages:

- The original deployment continues running and production work can be uninterrupted.
- You can test the new database out of production and act on any application incompatibilities.
- The entire process can be rerun at any point.
- A fresh restoration reduces the likelihood that unneeded artifacts of the older version are carried over to the new deployment.

## Upgrading in the UI

You can upgrade to a new version when [restoring a backup](/docs/messages-for-rabbitmq?topic=cloud-databases-dashboard-backups#restoring-a-backup) from the _Backups_ tab of your _Deployment Overview_. Clicking **Restore** on a backup brings up a dialog box where you can change some options for the new deployment. One of them is the database version, which is auto-populated with the versions available for you to upgrade to. Select a version and click **Restore** to start the provision and restore process.

## Upgrading through the CLI

When you upgrade and restore from backup through the  {{site.data.keyword.cloud_notm}} CLI, use the provisioning command from the resource controller.
```
ibmcloud resource service-instance-create <service-name> <service-id> <service-plan-id> <region>
```
The parameters `service-name`, `service-id`, `service-plan-id`, and `region` are all required. You also supply the `-p` with the version and backup ID parameters in a JSON object. If you need to use a key protect key, resize the deployment, or allocate dedicated cores, you can do so with the optional parameters `key_protect_key`, `members_disk_allocation_mb`, `members_memory_allocation_mb`, and/or `members_cpu_allocation_count`, and their desired values to the body of the request.
```
ibmcloud resource service-instance-create example-upgrade messages-for-rabbitmq standard us-south \
-p '{"backup_id": "crn:v1:bluemix:public:messages-for-rabbitmq:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:06392e97-df90-46d8-98e8-cb67e9e0a8e6", "version":3.8}'
```

## Upgrading through the API

Similar to provisioning through the API, you need to complete [the necessary steps to use the resource controller API](/docs/databases-for-postgresql?topic=cloud-databases-provisioning#provisioning-through-the-resource-controller-api) before you can use it to upgrade from a backup. Then, send the API a POST request. The parameters `name`, `target`, `resource_group`, and `resource_plan_id` are all required. You also supply the version and backup ID. If you need to use a key protect key, resize the deployment, or allocate dedicated cores, you can do so with the optional parameters `key_protect_key`, `members_disk_allocation_mb`, `members_memory_allocation_mb`, and/or `members_cpu_allocation_count`, and their desired values to the body of the request.
```
curl -X POST \
  https://resource-controller.bluemix.net/v2/resource_instances \
  -H 'Authorization: Bearer <>' \
  -H 'Content-Type: application/json' \
    -d '{
    "name": "my-instance",
    "target": "bluemix-us-south",
    "resource_group": "5g9f447903254bb58972a2f3f5a4c711",
    "resource_plan_id": "messages-for-rabbitmq-standard",
    "backup_id": "crn:v1:bluemix:public:messages-for-rabbitmq:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:06392e97-df90-46d8-98e8-cb67e9e0a8e6",
    "version":3.8
  }'
```

