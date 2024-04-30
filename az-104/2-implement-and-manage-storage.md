# Implement and manage storage

***

## Configure storage accounts

### Implement Azure Storage

#### Things to know about Azure Storage

| Category             | Description                                                                                                                                                                                            | Storage Examples                                                                                                                                                                                                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Virtual machine data | Virtual machine data storage includes disks and files. Disks are persistent block storage for Azure IaaS virtual machines. Files are fully managed file shares in the cloud.                           | Storage for virtual machine data is provided through Azure managed disks. Data disks are used by virtual machines to store data like database files, website static content, or custom application code. The number of data disks you can add depends on the virtual machine size. Each data disk has a maximum capacity of 32,767 GB. |
| Unstructured data    | Unstructured data is the least organized. Unstructured data may not have a clear relationship. The format of unstructured data is referred to as nonrelational.                                        | Unstructured data can be stored by using Azure Blob Storage and Azure Data Lake Storage. Blob Storage is a highly scalable, REST-based cloud object store. Azure Data Lake Storage is the Hadoop Distributed File System (HDFS) as a service.                                                                                          |
| Structured data      | Structured data is stored in a relational format that has a shared schema. Structured data is often contained in a database table with rows, columns, and keys. Tables are an autoscaling NoSQL store. |                                                                                                                                                                                                                                                                                                                                        |

#### Things to consider when using Azure Storage

* Consider durability and availability. Azure Storage is durable and highly available. Redundancy ensures your data is safe during transient hardware failures. You replicate data across datacenters or geographical regions for protection from local catastrophe or natural disaster. Replicated data remains highly available during an unexpected outage.
* Consider secure access. Azure Storage encrypts all data. Azure Storage provides you with fine-grained control over who has access to your data.
* Consider scalability. Azure Storage is designed to be massively scalable to meet the data storage and performance needs of modern applications.
* Consider manageability. Microsoft Azure handles hardware maintenance, updates, and critical issues for you.
* Consider data accessibility. Data in Azure Storage is accessible from anywhere in the world over HTTP or HTTPS. Microsoft provides SDKs for Azure Storage in various languages. You can use .NET, Java, Node.js, Python, PHP, Ruby, Go, and the REST API. Azure Storage supports scripting in Azure PowerShell or the Azure CLI. The Azure portal and Azure Storage Explorer offer easy visual solutions for working with your data.

### Explore Azure Storage services

Azure Blob Storage (containers): A massively scalable object store for text and binary data.

Azure Files: Managed file shares for cloud or on-premises deployments.

Azure Queue Storage: A messaging store for reliable messaging between application components.

Azure Table Storage: A service that stores nonrelational structured data (also known as structured NoSQL data).

### Determine storage account types

### Determine replication strategies

We explore four replication strategies:

* Locally redundant storage (LRS)
* Zone redundant storage (ZRS)
* Geo-redundant storage (GRS)
* Geo-zone-redundant storage (GZRS)

#### Things to consider when choosing replication strategies

| Event                                 | LRS | ZRS | GRS | RA-GRS | GZRS | RA-GZRS |
| ------------------------------------- | --- | --- | --- | ------ | ---- | ------- |
| Node in data center unavailable       |     |     |     |        |      |         |
| Entire data center unavailable        |     |     |     |        |      |         |
| Region-wide outage                    |     |     |     |        |      |         |
| Read access during region-wide outage |     | ZRS | GRS | RA-GRS | GZRS | RA-GZRS |

![alt text](../res/1.%20Manage%20Azure%20identities%20and%20governance/images/image.png)

### Access storage

* Every object you store in Azure Storage has a unique URL address. Your storage account name forms the subdomain portion of the URL address. The combination of the subdomain and the domain name, which is specific to each service, forms an endpoint for your storage account.
* To access the myblob data in the mycontainer location in your storage account, we use the following URL address:

//mystorageaccount.blob.core.windows.net/mycontainer/myblob.

| Service           | Default endpoint                          |
| ----------------- | ----------------------------------------- |
| Container service | //mystorageaccount.blob.core.windows.net  |
| Table service     | //mystorageaccount.table.core.windows.net |
| Queue service     | //mystorageaccount.queue.core.windows.net |
| File service      | //mystorageaccount.file.core.windows.net  |

#### Configure custom domains

* You can configure a custom domain to access blob data in your Azure storage account. As we reviewed, the default endpoint for Azure Blob Storage is \<storage-account-name>.blob.core.windows.net. If you map a custom domain and subdomain, such as www.contoso.com, to the blob or web endpoint for your storage account, your users can use that domain to access blob data in your storage account.
* There are two ways to configure a custom domain:
  * Direct mapping
  * Intermediary domain mapping.

### Secure storage endpoints

#### Things to know about configuring service endpoints

Here are some points to consider about configuring service access settings:

* The Firewalls and virtual networks settings restrict access to your storage account from specific subnets on virtual networks or public IPs.
* You can configure the service to allow access to one or more public IP ranges.
* Subnets and virtual networks must exist in the same Azure region or region pair as your storage account.

***

## Configure Azure Blob Storage
