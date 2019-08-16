# Overview {#concept_f4z_knq_tdb .concept}

POLARDB is a next-generation cloud-based service developed by Alibaba Cloud for relational databases, which is fully compatible with MySQL. It is developed based on a distributed storage architecture and delivers up to six times throughput of MySQL. POLARDB provides high-capacity, low-latency online transaction processing \(OLTP\) services. It also offers cost-effective and scalable services.

## Basic concepts {#section_fkb_nnq_tdb .section}

-   **Cluster**: A POLARDB cluster contains one primary instance and a maximum of 15 read-only instances \(at least one, in order to provide active-active high availability support\). A POLARDB cluster ID starts with pc, which stands for POLARDB cluster.

-   **Instance**: An instance is an independent database server in which you can create and manage multiple databases. An instance ID starts with pi, which stands for POLARDB instance.

-   **Database**: A database is a logical unit created in an instance. The name of each POLARDB database under the same instance must be unique.

-   **Region and zone**: Each region is a separate geographic area. Zones are distinct locations within a region that operate on independent power grids and networks. For more information, see [Alibaba Cloud's Global Infrastructure](https://www.aliyun.com/about/global?spm=a2c4g.11186623.2.3.OXfiny).


## Console {#section_p15_lnq_tdb .section}

Alibaba Cloud offers a web-based and easy-to-use console where you can manage various products and services including POLARDB. In the console, you can create, access, and configure your POLARDB database.

For more information about the console layout, see [Alibaba Cloud console](https://help.aliyun.com/document_detail/47605.html).

The logon page for the POLARADB console is [https://polardb.console.aliyun.com](https://polardb.console.aliyun.com/).

