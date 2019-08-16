# FAQs {#concept_iyn_m3v_tdb .concept}

**What is POLARDB?**

POLARDB is a MySQL-compatible relational database service, with a focus on online transactional processing \(OLTP\) scenarios.

**\[DO NOT TRANSLATE\]**

\[DO NOT TRANSLATE\]

**Is data storage separate from compute processes in the POLARDB architecture?**

Yes. The decoupling of the compute and storage pools improves user experience for high availability, data backups, fault recovery, and scalability.

**What is the maximum storage limit of a POLARDB database?**

POLARDB supports a capacity of up to 100 TB per database instance.

**How does POLARDB perform an automated failover?**

When you purchase a POLARDB cluster, you will obtain a primary instance and a read-only instance. If a primary instance fails, the system will automatically promote the read-only instance to become primary while restoring the primary instance. If a read-only instance fails, the system will automatically create a replacement while restoring the faulty instance.

**What method is used in POLARDB for data backups?**

Snapshots are used in POLARDB for data backups.

**What is the maximum number of read-only instances I can have in POLARDB?**

You can purchase up to 15 read-only instances per POLARDB cluster.

**How long does it take to create a read-only instance?**

It only takes 2-5 minutes to create a read-only instance. regardless of your data volume.

**What protocol for high-speed networks is used in the POLARDB architecture?**

POLARDB uses dual-port Remote Direct Memory Access \(RDMA\) protocol to ensure high I/O throughput between DB servers, chunk servers, and data replicas. Each port can deliver up to 25 Gbps with low latency.

