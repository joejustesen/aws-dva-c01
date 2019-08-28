# DynamoDB

## General

- stored on ssd
- spread across 3 availability zones?
- 2 consitency models
  - eventual consistency (default)
    synced all version within a second
  - strong consistency
- made up of
  - tables
  - items
  - attributes
  - key-value
  - document
    - JSON
    - HTML
    - XML
  - keys used to store/retieve data based on Primary Key
    - partition key
    - composite key

## Indices

- local secondary index
  - must be created when creating your table, same partition key as your table, but has a different sort key
- global secondary index
  - create any time
  - can have different partition key

## API calls

- scans
  - examples all items in the table
  - can use ProjectionExpression to select specific attributes
  - can filter on any attribute
  - for large tables, can use up all provisioned IOPS for a single scan
  - set small page size to reduce opration
  - by default scans one partition at a time
  - can parallel scan by dividing table into segments and then parallel scaning those segments
  - avoid parallel scans if table or index is busy (read/write)
- queries
  - find items in table based on primary key and any distinct values
  - ProjectionExpression to select specific attributes
  - ScanIndexForward controls sort order (asc/desc), only on queries
  - can specify query is strong consistency

## Provisioned Throughput

- measured in capacity units
- set read and write capacity units (unless set to auto scaling)
- write capacity unit = 1 KB write per second
- read capacity unit = 4 KB strong consistent read or 2x4 KB eventually consistent read (default)

## On-Demand Capacity

- don't specify capacity units
- scales up and down based on activity
- great for unpredictable workloads, or large spikes
- pay for what you use
- can switch once per day (provisioned vs on-demand)

## DynamoDB Accelerator (DAX)

- fully managed, clustered, in-memory cache for DyanmoDB
- up to 10x read performance
- microsecond performance for millions of requests per second
- read heavy or bursty applications (example: black Friday promotions)
- write through cache service
- can reduce provisioned read capacity
- eventually consistent reads only
- uses write through strategy

## Elasticache

- use DAX if possible for DynamoDB
- in memory caching, (RDS or DynamoDB)
- reduce read load on database
- lowers latency access
- types
  - Memcached
    - no multi-AZ
    - multi-threaded
  - Redis
    - key-value store
    - complex data structures
    - master/slave and multi-AZ redundency
- strategies
  - Lazy Loading
    - only loads requested data into cache
    - returns NULL if not in cache
    - can get stale data
    - use TTL to eject possible stale data
  - Write Through
    - data never stale
    - write penalty
    - write all updates to cache as well as the database
    - only written data is in the cache
    - possible wasted data if written data is not usually read again

## Transactions

- ACID

## TTL - Time To Live

- data can expire
- expired data will be removed in the next 24 hours
- good for:
  - session data
  - event logs
  - temporary data
- can reduce storage costs
- in epoch time (unix timestamp)

## Streams

- time ordered sequence of item level modifications (insert, update, delete)
- recorded as logs
- events only stored for 24 hours
- use normally to track events to trigger actions (lambda functions)
- Primary Key or before after images of item
- different end point for stream
- recorded in near real time
- event source for lambda

## Errors and Exponential Backoff

- ProvisionedThroughputExceededException
- SDK automatically retries until successful
- Not using SDK,
  - reduce request frequency
  - implement Exponential Backoff
- might be caused by a request that is to large
