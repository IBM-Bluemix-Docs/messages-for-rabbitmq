---
copyright:
  years: 2019, 2020
lastupdated: "2020-10-01"

keywords: rabbitmq, databases, jms, shovel, delayed, stomp

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Using RabbitMQ plug-ins
{: #plugins}

RabbitMQ supports various plug-ins to extend its core functions. {{site.data.keyword.messages-for-rabbitmq_full}} comes with a selection of plug-ins that are already enabled on your deployment. Plug-in management is handled by the {{site.data.keyword.messages-for-rabbitmq}} service. Users cannot enable or disable plug-ins.

## Shovel plug-in

{{site.data.keyword.messages-for-rabbitmq}} comes with the [Shovel plug-in](https://www.rabbitmq.com/shovel.html) and the [Shovel Management plug-in](https://github.com/rabbitmq/rabbitmq-shovel-management) enabled. You can configure the plug-in through both the [RabbitMQ Management plug-in UI](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-management-plugin) and its accompanying API.

The _Shovel Status_ and _Shovel Management_ links appear under the _Admin_ tab.

![Admin tab with the Shovel plug-in](images/plugins-shovel-ui.png)

If you do not see the _Admin_ tab, you might need to log in to the management UI with the [admin user](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-admin-password). 
{: .tip}

In the RabbitMQ Management API, the Shovel Management plug-in adds endpoints for listing, creating, and deleting shovels. Usage and examples are in the [GitHub repository's documentation](https://github.com/rabbitmq/rabbitmq-shovel-management#usage).

## Delayed Message plug-in

The [delayed message plug-in](https://github.com/rabbitmq/rabbitmq-delayed-message-exchange) is a third-party plug-in that adds delayed messaging and scheduled messaging to RabbitMQ. 

To use the plug-in, declare an exchange with the type `x-delayed-type`. To delay a message, publish it with the `x-delay` header with the number of milliseconds to delay the message. More detailed usage information is in the [plug-in's documentation](https://github.com/rabbitmq/rabbitmq-delayed-message-exchange#usage).

## STOMP plug-in

The [RabbitMQ STOMP plug-in](https://www.rabbitmq.com/stomp.html) supports sending [STOMP-formatted](http://stomp.github.io/) messages through RabbitMQ. The plug-in enables a port to handle STOMP traffic on your deployment, and it is TLS/SSL secured. The connection information for STOMP clients is in the `stomp_ssl` section of your deployment's [connection strings](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings#the-stomp_ssl-section).

## RabbitMQ Management plug-in

The Management plug-in provides access to your deployment through a web browser, `rabbitmqadmin` and through the RabbitMQ API. Information on using the Management plug-in to connect to your deployment in on the [Connecting with the RabbitMQ Management plug-in](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-management-plugin) page.

## JMS plug-in

The RabbitMQ JMS Topic Exchange plug-in is enabled by default for {{site.data.keyword.messages-for-rabbitmq}} deployments. This plug-in adds server-side support for the [RabbitMQ JMS client](https://github.com/rabbitmq/rabbitmq-jms-client) and supports JMS topic routing plus selection based on JMS SQL selection rules.

The RabbitMQ JMS Client is required to communicate with the plug-in. Review the [JMS Client documentation page](https://www.rabbitmq.com/jms-client.html) that is provided by RabbitMQ for more detailed information on installation and configuration, along with examples.

More detailed information about the JMS plug-in can also be found in the RabbitMQ JMS Topic Exchange plug-in [GitHub repo](https://github.com/rabbitmq/rabbitmq-jms-topic-exchange). 


