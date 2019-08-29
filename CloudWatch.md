# CloudWatch

## Monitors
- compute
    - Autoscaling groups
    - elastic load balancers
    - Route53 Health Checks
- storage
    - EBS volumes
    - storage gateways
    - CloudFront
- other
    - SNS topics
    - SQS queues
    - Opsworks
    - logs
    - estimated billing charges
- EC2 metrics
    - defaults to 5 minute updates, can be reduced to 1 minute
    - CPU
    - Network
    - Disk
    - Status Checks
    - NOT RAM or disk usage levels
- metrics
    - detail, every 1 minutes
    - normal, every 5 minutes
    - custom minimum interval is 1 minute
- alarms
    - monitor any metric, including billing
- storage
    - default is logs are never deleted
- tips
    - can send data from on prem, need to install agent first


## CloudTrail
- monitors API calls,
- used for auditing

## Config
- audit changes to your resources
- can notify of changes to resources