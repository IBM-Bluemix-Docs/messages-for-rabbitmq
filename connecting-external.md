---
copyright:
  years: 2017,2018
lastupdated: "2018-10-26"

keywords: rabbitmq, databases

subcollection: messages-for-rabbitmq

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #external-app}

Your applications and drivers use connection strings to make a connection to {{site.data.keyword.messages-for-rabbitmq_full}}. Your deployment has connection strings specifically for drivers, clients, and applications. Connection strings are displayed in the _Connections_ panel of your deployment's _Overview_, and can also be retrieved from the [cloud databases CLI plugin](/docs/databases-cli-plugin?topic=cloud-databases-cli-cdb-reference#deployment-connections), and the [API](https://{DomainName}/apidocs/cloud-databases-api#discover-connection-information-for-a-deployment-f-e81026).

The connection strings can be used by any of the credentials you have created on your deployment. While you can use the admin user for all of your connections and applications, it might be better to create users specifically for your applications to connect with. Documentation on creating users is on the [Creating Users and Getting Connection Strings](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-connection-strings) page.

## Connecting with a language's driver

The information a driver needs to make a connection to your deployment is in the `amqps` section of your connection strings. The table contains a breakdown for reference.

Field Name|Index|Description
----------|-----|-----------
`Type`||Type of connection - for RabbitMQ, it is `uri`
`Scheme`||Scheme for a URI - for RabbitMQ, it is `amqps`
`Path`||Path for a uri
`Authentication`|`Username`|The username that you use to connect.
`Authentication`|`Password`|A password for the user - might be shown as `$PASSWORD`
`Authentication`|`Method`|How authentication takes place; "direct" authentication is handled by the driver.
`Hosts`|`0...`|A hostname and port to connect to
`Composed`|`0...`|A URI combining Scheme, Authentication, Host, and Path
`Certificate`|`Name`|The allocated name for the self-signed certificate for database deployment
`Certificate`|`Base64`|A base64 encoded version of the certificate.
{: caption="Table 1. `RabbitMQ`/`uri` connection information" caption-side="top"}

* `0...` indicates that there might be one or more of these entries in an array.

Many RabbitMQ drivers are able to make a connection to your deployment when given the URI-formatted connection string found in the "composed" field of the connection information. For example,
```
amqps://$USERNAME:$PASSWORD@f08da56c-f975-4cad-98a5-633b8b5a8e79.974350db55ab4ec0983f023940bf637f.databases.appdomain.cloud:30402
```

The table covers a few of the common RabbitMQ drivers.

Language|Driver|Documentation
----------|-----------
Node|`amqplib`|[Link](https://www.npmjs.com/package/amqplib)
Java|RabbitMQ Java Client Library|[Link](http://www.rabbitmq.com/java-client.html)
Ruby|`Bunny`|[Link](http://rubybunny.info/)
Python|`pika`|[Link](https://pika.readthedocs.io/en/stable/)
{: caption="Table 2. Common RabbitMQ drivers" caption-side="top"}

## Connecting with a `STOMP` client

The information a STOMP client needs to make a connection to your deployment is in the `stomp_ssl` section of your connection strings. The table contains a breakdown for reference.

Field Name|Index|Description
----------|-----|-----------
`Type`||Type of connection - for STOMP, it is `stomp`
`Authentication`|`Username`|The username that you use to connect.
`Authentication`|`Password`|A password for the user - might be shown as `$PASSWORD`
`Authentication`|`Method`|How authentication takes place; "direct" authentication is handled by the client.
`Hosts`|`0...`|A hostname and the STOMP-enabled port to connect to, as well as the protocol name "stomp-ssl"
`Composed`|`0...`|A URI combining Authentication, Host, and TLS/SSL
`ssl`||The TLS/SSL setting needed for a connection. Should always be `true`.
`Certificate`|`Name`|The allocated name for the self-signed certificate for database deployment
`Certificate`|`Base64`|A base64 encoded version of the certificate.
{: caption="Table 2. `RabbitMQ`/`stomp_ssl` connection information" caption-side="top"}

* `0...` indicates that there might be one or more of these entries in an array.

## Connecting with an `MQTT` client

The information that an MQTT client uses to connect can be found in the `mqtts` section of your connection strings. The table contains a reference.

The "mqtts" section contains the information that an MQTT client needs to connect to your deployment.

Field Name|Index|Description
----------|-----|-----------
`Type`||Type of connection - for `MQTTS`, it is `uri`.
`Scheme`|| Scheme for a URI - in this case it is `mqtts`.
`Authentication`|`Username`|The username that you use to connect.
`Authentication`|`Password`|A password for the user - might be shown as `$PASSWORD`
`Authentication`|`Method`|How authentication takes place; "direct" authentication is handled by the driver.
`Hosts`|`0...`|A hostname and port to connect to.
`Composed`|`0...`|A URI combining Authentication, Host, and Port used to connect.
`Certificate`|`Name`|The allocated name for the self-signed certificate for database deployment
`Certificate`|`Base64`|A base64 encoded version of the certificate.
{: caption="Table 2. `RabbitMQ`/`mqtts` connection information" caption-side="top"}

* `0...` indicates that there might be one or more of these entries in an array.

## TLS and self-signed certificate support

All connections to {{site.data.keyword.messages-for-rabbitmq}} are TLS 1.2 enabled, so the driver or client you use to connect needs to be able to support encryption. Your deployment also comes with a self-signed certificate so the driver can verify the server upon connection. 

### Using the self-signed certificate

1. Copy the certificate information from the _Connections_ panel or the Base64 field of the connection information. 
2. If needed, decode the Base64 string into text. 
3. Save the certificate  to a file. (You can use the Name that is provided or your own file name).
4. Provide the path to the certificate to the driver or client.
5. (optional) If your driver or client supports it you can add the certificate its (or your system's) certificate store.

### CLI plug-in support for the self-signed certificate

You can display the decoded certificate for your deployment with the CLI plug-in with the command `ibmcloud cdb deployment-cacert "your-service-name"`. It decodes the base64 into text. Copy and save the command's output to a file and provide the file's path to the driver or client.






 
