---

Copyright:
  years: 2018
lastupdated: "2018-11-21"

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# About {{site.data.keyword.messages-for-rabbitmq_full_notm}}
{: #about}

{{site.data.keyword.messages-for-rabbitmq_full}} is a managed RabbitMQ service that is hosted in the {{site.data.keyword.cloud_notm}} and integrated with other {{site.data.keyword.cloud_notm}} services. 
{:shortdesc}

## Provisioning {{site.data.keyword.messages-for-rabbitmq}}

{{site.data.keyword.messages-for-rabbitmq}} is an {{site.data.keyword.cloud_notm}} service. Provisioning and account management is handled through your {{site.data.keyword.cloud_notm}} account. If you already have an account, you can provision {{site.data.keyword.messages-for-rabbitmq}} from the [{{site.data.keyword.cloud_notm}} catalog](https://{DomainName}/catalog/services/messages-for-rabbitmq).

For detailed provisioning information, including {{site.data.keyword.cloud_notm}} CLI instructions, see the [Provisioning](/docs/services/messages-for-rabbitmq?topic=cloud-databases-provisioning) page.

If you don't yet have an {{site.data.keyword.cloud_notm}} account, sign up on the [registration](https://{DomainName}/registration/) page.

### Managing Access to {{site.data.keyword.messages-for-rabbitmq}}

{{site.data.keyword.messages-for-rabbitmq}} is an Identity and Access Management (IAM) integrated service. Access to the service is governed by the roles and attributes that are consistent across IAM-integrated services in {{site.data.keyword.cloud_notm}}. Get started with managing your users on the [IAM Getting Started tutorial](/docs/iam?topic=iam-getstarted). For more information about IAM, see the [What is IAM?](/docs/iam?topic=iam-iamoverview) documentation.

More information on IAM roles and actions for the {{site.data.keyword.messages-for-rabbitmq}} service is available on the [Access Management Integration](/docs/services/messages-for-rabbitmq?topic=cloud-databases-iam) page.

## Using {{site.data.keyword.messages-for-rabbitmq}}

{{site.data.keyword.messages-for-rabbitmq}} provides a UI, accessible by selecting _Manage_ from the left sidebar of your service and opening the management panel. You get a quick [Overview](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-dashboard-overview) of your service as well as configuration settings on the [Settings](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-dashboard-overview#settings) tab and access to your backups on the [Backups](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-dashboard-backups) tab.

### Using the {{site.data.keyword.cloud_notm}} command-line interface

The [{{site.data.keyword.cloud_notm}} command-line interface](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli) provides an interactive terminal for your {{site.data.keyword.cloud_notm}} account and your {{site.data.keyword.cloud_notm}} services. The cloud databases plug-in extends this functionality to your {{site.data.keyword.messages-for-rabbitmq}} deployments. More information and installation instructions are on the [{{site.data.keyword.cloud_notm}} CLI Plug-in](/docs/databases-cli-plugin?topic=cloud-databases-cli-cdb-reference) page.

### Using the cloud databases API

{{site.data.keyword.messages-for-rabbitmq}} is compatible with the {{site.data.keyword.IBM_notm}} {{site.data.keyword.databases-for}} API, so you can access and manage your service programmatically. Each region has a unique endpoint, so you can find the API foundation endpoint for your deployment on the [_Overview_](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-dashboard-overview) page. The {{site.data.keyword.IBM_notm}} API documentation contains the full [{{site.data.keyword.databases-for}} API reference](https://{DomainName}/apidocs/cloud-databases-api). Authentication is IAM-based and you use your {{site.data.keyword.cloud_notm}} account's platform API keys to access the API. More information on API keys is in the [IAM documentation](/docs/iam/apikeys?topic=iam-manapikey).

## Connecting to {{site.data.keyword.messages-for-rabbitmq}}

General information on getting connection strings can be found on the [Getting Connection Strings](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings) page.

{{site.data.keyword.messages-for-rabbitmq}} deployments are secured with authentication and SSL/TLS encrypted connections. Deployments are provisioned with an admin user. [Set the admin password](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-admin-password) to use it to access your deployment. The RabbitMQ management plugin enabled on deployments by default. If you want to manage the RabbitMQ through the browser or the command-line, [connect by using the RabbitMQ Management Plugin](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-management-plugin).

Specific guidance on connecting with RabbitMQ drivers is on the [Connecting External Applications](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-external-app) page. If you want to connect a Cloud Foundry application that is running in {{site.data.keyword.cloud_notm}}, see the [Connecting an {{site.data.keyword.cloud_notm}} Application](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-ibmcloud-app) page. The [Getting Started tutorial](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started) provides a sample application that can run locally or on {{site.data.keyword.cloud_notm}} to test-drive your {{site.data.keyword.messages-for-rabbitmq}} deployment.

## Other {{site.data.keyword.cloud_notm}} Integrations

{{site.data.keyword.messages-for-rabbitmq}} deployments offer other cloud services integrations. 
- View events with [Activity Tracker](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-activity-tracker)
- Monitor deployment resource use with the [Monitoring](/docs/services/messages-for-rabbitmq?topic=cloud-databases-monitoring) service.
- BYOK encryption is available if you use [Key Protect](/docs/services/messages-for-rabbitmq?topic=cloud-databases-key-protect)
- [Service Endpoints Integration](/docs/services/messages-for-rabbitmq?topic=cloud-databases-service-endpoints) allows you to select public or private networking for your deployment at provision