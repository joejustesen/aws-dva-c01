# Other

## SQS

- pull based system
- max 256 KB message size
- decouples producer and consumer of messages
- types
  - standard (default)
    - unlimited TPS
    - not ordered, best effort
    - a least one message deliveried
  - fifo
    - ordered perserved
    - limited to 300 TPS
- message lifetime 1 minute to 14 days, default is 4 days
- visiblity timeout, time message is invisible after it has been picked up a reader
  - default 30 seconds
  - max 12 hours
- polling
  - short polling
  - long polling
    - waits for message or timeout

## SNS - Simple Notification Service

- push notification
  - SMS
  - email
  - SQS
  - HTTP endpoint
  - lambda function
- pub/sub model
- topics
  - multiple subscribers
  - stored redundantly
- pay as you go,
  - \$0.50 per 1 million requests
  - \$0.06 per 100,000 HTTP notifications
  - \$0.75 per 100 SMS notifications
  - \$2.00 per 100,000 emails

## SES - Simple Email Service

- pay as you go
- can receive emails delivered to S3 bucket
- incoming emails can trigger lambda or SNS notifications

## Kinesis

- streaming data service
- load and analyze stream data
- types of streams
  - Video
    - not covered ??
  - Streams
    - store for 24 hours (default) up to 7 days
    - stored in shards
    - consumers
      - EC2, Lambda, EMR, Kinesis Data Analytics
    - a single shard
      - reads 5 TPS, up to 2 MB per second
      - writes 1000 TPS, up to 1 MB per second
      - 10 shards limited per region
  - Firehose
    - automated streams
    - no data retention
    - data sent to S3 or Elasticsearch Cluster
  - Analytics
    - SQL queries of dta
    - store query results into S3, RedShift, Elasticsearch Cluster

## Systems Manager Parameter Store

- versioned key value store
- standard
  - up to 10,000 parameters
  - 4 KB max values size
- advanced
  - more than 10,000 parameters
  - 8 KB max values size
- value types
  - String
  - StringList
  - SecureString
    - Encrypt using KMS key
