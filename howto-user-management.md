---
copyright:
  years: 2019
lastupdated: "2019-02-05"

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Managing Users
{: #user-management}

{{site.data.keyword.messages-for-rabbitmq_full}} uses RabbitMQ's [built-in access control](https://www.rabbitmq.com/access-control.html#permissions). 

When you provision a new deployment in {{site.data.keyword.cloud_notm}}, you are automatically given an admin user to access and manage RabbitMQ. You can also add users in the _Service Credentials_ panel, which allows for access to RabbitMQ to be integrated with your {{site.data.keyword.cloud_notm}} account and [IAM](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-iam).

Since {{site.data.keyword.messages-for-rabbitmq}} comes with the RabbitMQ Management Plugin enabled, users' access is also controlled by [user tags](https://www.rabbitmq.com/management.html#permissions). These tags control what information is available to users through the management UI, `rabbitmqadmin`, and the RabbitMQ HTTP API.

## The admin user

Every RabbitMQ deployment comes with an admin user. This admin user had full administrative privileges on your RabbitMQ deployment. Before you log in with the admin user, you need to [set its password](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-admin-password).

The biggest difference between the admin user and any other users you add to your deployment is the ability to provision new vhosts and manage all other users' permissions and access. 

It is the only user that is initially granted access to all the settings and configuration that is found in the _Admin_ tab in the management UI. 

## _Service Credential_ Users

Users that you [create through the _Service Credentials_ panel](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings#generating-connection-strings-from-service-credentials) are given full permissions to configure, write, and read on the default Virtual Host.  

They are also automatically tagged with the "monitoring" tag, allowing them users to access the management plugin and see all connections and channels as well as node-related information. These users given a limited view of the _Admin_ tab and the functions that are found there. 

If you need users that are created from _Service Credentials_ to have more privileges, you can log in with the admin user and grant them.

## RabbitMQ Users

You can bypass creating users in _Service Credentials_ and create users directly in RabbitMQ. The RabbitmQ Management Plugin UI has a tab for user creation and management available to the admin user on your deployment.

Users created directly in RabbitMQ do not appear in _Service Credentials_, but you can [add them there](/docs/services/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings#generating-service-credentials-for-existing-users) if you choose. Note, that these users will not be integrated with IAM controls, even if added to _Service Credentials_.

## The `ibm` user

If you log into the management UI with your admin account, you might have noticed a user that is named `ibm`. The `ibm` user is the internal administrative account that manages replication, metrics, and other functions that ensure the stability of your deployment. It has the same permission levels and tags as the provided admin user. Changes to the `ibm` account are not advised and can disrupt the availability of your deployment.