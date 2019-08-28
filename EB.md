# Elastic Beanstalk

## Overview

- supports
  - Java,
  - .NET
  - php
  - Node.js
  - Python
  - Ruby
  - Go
  - Docker
  - platforms (Tomcat, Passenger, Puma, IIS)
- handles deployment, capacity planning, load balancing, auto-scaling and application health
- runs from S3 bucket
- fastest way to deplay application to AWS
- control EC2 yourself or allow ELB to control EC2 resources
- integrated with CloudWatch and X-Ray

## Deployment Policies

- all at once
  - new verions to all instances
  - causes down time
  - failed updates require redeploy of prior verions
  - (use in test/dev)
- rolling
  - deploys in batches
  - failed updates require rolling update of prior version
  - not for performance sensitive systems
- rolling with additional batch
  - maintains full capacity
  - adds instances that are updated
  - full capacity/no downtime/no performance degredations
- immutable
  - deploys to fresh auto scaling group of instances
  - pass health checks, moved to existing auto scaling group
  - preferred for mission critical production systems

## Configuration

- saved in .ebextensions folder in top level of zip/S3
- .config files in folder

## RDS

- launch RDS instance within EB
  - good for devb/test
  - RDS coupled EB, delete of EB environment deletes RDS instances
- Normal RDS instance
  - Add RDS security group to EB auto scaling group
  - provide RDS connection string to application servers using EB environment properties
