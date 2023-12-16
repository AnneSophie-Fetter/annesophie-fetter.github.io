---
layout: post
title: "Key-Value vs Columnar storage"
categories: "big-data-fundamentals"
---


On scaling data stores to multiple machines, we face new challenges on how the data can be structured. A number of usual features from relational databases cannot be applied:

- Foreign Keys (aka “relations”): when writing, we would have to find the matching records between the 2 tables to check the relation is valid across the cluster, which increases the latency.
And when reading, the data has to travel across the network (“shuffling”) if the relation is used.
- Field value indexing: not a limitation brought by distribution per se, but by the size of the data stored.
Having indexes on arbitrary fields increases the amount of RAM used to guarantee fast retrieval, which does not scale efficiently.


## Key-Value Stores

The data record has a key and a value (the value can be a set of fields or a document).
The key is used to know which node should hold the value, and it is included in the index of the node to enable fast retrieval of the value.  

This means the client writing or reading an individual record only interacts with a single node.
No data is shuffled across the network, therefore the latency of read/write operations is extremely low, even if we are interacting with a distributed system.  

The counterpart is that we cannot query the data unless we know the key we are looking for.
Filters, aggregations or joins on another field than the key will incur massive amounts of scanning across all the nodes, and therefore poor performance  

## Columnar Stores

To enable filters, aggregations and joins on distributed systems, we can store data in a “columnar” fashion.
Each field is stored separately from the others in a single column (a row number is used to keep track of which record the value belongs to).  
Now when filtering, aggregating and joining only the columns used in these operations are scanned.  

To improve performance these columns are split in “blocks” of values, which carry metadata: min, max, average, bloom filter index etc...
These statistics are used to discard early any block that does not contain the values we are looking for.  

The drawback is that writing to the store requires to re-organize the blocks, and update the metadata.
This means it cannot be used for fast writing. Similarly, as there is no index, the retrieval of a single record requires all nodes to go through their blocks and find the values of the record.  

## Summary:

### Key-Value:

- Fast Read/Write
- Cannot filter, aggregate and join based on value fields

### Columnar:

- Slow Read/Write
- Enables filters, aggregations and joins on any field

### End notes

- Elasticsearch is a peculiar case, it is technically a document store (hear “key-value where the value is a JSON document”). But all the fields are indexed by default. As said previously, this causes increased memory usage and write latency. However the consequence is a very low latency on read/search queries, therefore this can be an acceptable trade-off.
- Key-Value stores are called “NoSQL” because of the lack of SQL-typical operations. Backend services can denormalize the data (put all the relational information in the same record), and store it in Key-Value stores without SQL operations, as long as the key is known (a user_id for example). However the lack of schema validation can cause problems if the backend service does not do it itself.
- Columnar stores can make use of multiple additional strategies to improve performances which may not be standard across all systems: partitioning the data, block sorting, data co-location using a field hash…
- Columnar stores can be as simple as a collection of files on a block/object storage, and read through a query engine like Presto, Drill, Hive etc…