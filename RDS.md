# RDS

- All db engines use EBS volumnes except Aurora
- database identifier must be unique for account in a region
- every database gets a master account, don't use for normal use
- (OLTP) SQL Server, MySQL, PostgreSQL, Oracle, Aurora, MariaDB
- (OLAP) Redshift
- Elasticache [Memcached, Redis]

## Aurora

### Endpoints

- cluster endpoint, connects to the primary DB instance, read and write, uses DNS to identify primary instance, on failover, DNS CNAME is updated to new primary DB instance
- reader endpoint, connects to a read replica, DNS load balanced, read only
- instance endpoint, connects to a specific clustered instance, can read or read/write depending on the instance

### Engine

- Oracle (Standard, Standard 1, Standard 2, Enterprise)
- SQL Server (Express, Web, Standard, Enterprise)
- Aurora
- Postgresql
- MySQL
- MariaDB

### Use Case

- Production
  - Multi-AZ
- Dev/Test
  - Single AZ
  - Allocated Storage 20GB

### License

- Oracle BYO, or On-Demand (only Oracle has options)

### Instance Families

- Burstable
  - 1 to 8 vCPU
  - 1 to 32 GB RAM
- M3/M4 Family
  - general purpose
  - 2 to 64 vCPU
  - 8 to 256 GB RAM
- R3/R4 Family
  - Memory optimized
  - 2 to 64 vCPU
  - 16 to 488 GB RAM

### Storage

- General Purpose (GP2)
  - SSD
  - Max 16 TB
  - 3 IOPS per GB, larger DB, better performance
  - burst IOPS to 3000
- Provisioned IOPS (IO1)
  - SSD
  - Max 16 TB
  - Max 40K IOPS, (20K for SQL Server)
  - Production work loads
- Magnetic (rotational disks)
  - legacy
  - Max 16 TB

## Cost Drivers

- Instance hours
  - Region
  - Instance type
  - db engine and license
- Storage
  - EBS vs Aurora
  - Type (GP2/IO1/Magnetic)
  - GB of space
- Backup s
  - no charge < 100% of db storage size
- Data transfer
  - out going only
  - region to region

## Scaling database

- scale vertically, memory or cpu instance
  - new host attached to existing volumes
  - multi-az, secondary instances resized first
    - minimizes downsize
  - downtime
  - check commercial instance license if allowed
- scale EBS storage
  - no downtown
- scale read read replicas
  - only db engines that support read replicas
  - helps read traffic only
  - no downtime

## Multi-AZ

- high availability
- sync data writes between zones
- does not improve performance
- used for failovers
- writes slower
- twice the cost
- backups taken from secondary hosts, improves backup impact on production
- uses DNS CNAME records to direct to primary host
- test with reboot with failover option, check TTL
- failover can take 1 to 2 minutes
- failovers caused by:
  - AZ outage, unplanned
  - db instance fails, unplanned
  - change host class by user
  - patching software by AWS
  - manual host reboot by user
- check host instance
  - linux `host -t NS [endpoint]`
  - windows `nslookup [endpoint]`

## Read Replica

- use for read scaling, read heavy db
- 5 max read replicas per DB
- good for when master db is unavailable ??
- data warehousing and reporting
- cross region read replica good for lowering latency
- disaster recovery, can promote read replicas to master

## Backups

- encrypted if database is encrypted,
- restored instances have a different url
- automated
  - ebs volume snapshots are taken from secondary hosts (if multi-az) and saved to internal S3 bucket
  - point in time every 5 minutes
    - can rewind DB to point in time
    - uses transaction logs copied to S3 bucket
  - options
    - window
    - retention (1 to 35 days), default is 7 days
- manual
  - retention is up to the user
  - cannot rewind to point in time, best used before changes to DB
- snapshots are full volumes and then diffs
- performance
  - single az, I/O suspension (seconds to minutes)
  - multi-az no impact
- restore
  - creates a new DB
  - must retain parameter and security groups
  - change storage types will slow down restore
  - speed up by maximizing I/O during restore process

## Security

- network isolation
  - private subnets
  - security groups (firewalls)
  - turn off public access
  - ClassicLink
  - DirectConnect
  - VPC peering
- IAM
  - do not AWS root credentials
  - can use MFA
  - use DB tech within DB
  - AD for SQL Server
- encryption at rest
  - free, provided by AWS KMS, no performance impact, uses AES-256
  - replications are also encrypted
  - performed at volume level (EBS)
  - can rotate keys, but cannot unencrypt data once encrypted
  - (envelope keys) two tier encryption, master key created by user, each instance has its own key
- SSL for database connections

## Monitoring

- focus on key metrics
- RDS sends metrics to CloudWatch
- 1 min intervals
- alarms can trigger actions
- main metrics
  - cpu
  - storage space, should have > 20% free
  - network traffic
  - db connections
  - IOPS
- enhanced monitoring
  - host level metrics
  - 1 sec intervals (default is 60 sec)
  - 50 additional metrics
  - agent installed on host
- Performance Insights
  - identify DB bottlenecks
  - analyze queries, hosts, users
  - see impact of actions on server
  - free
  - not available on db.t2 instance classes
- AWS RDS Events
  - can be notified, subscribe to event
  - uses SNS
- AWS Config
- AWS CLoudTrail
- AWS Trusted Advisor

### RDS Elasticache

- store critical data in memory
- redis allows multi-az consistency
- redis is managed like a database, with persistence
- memcached auto scaling like EC2 auto scaling
- read heavy queries
- not for OLAP, use Redshift instead

#### Memcached

- simple
- offline database data
- scale out

#### Redis

- advanced data types (lists, hashes, sets)
- pub/sub
- sorting, ranked datasets like leaderboards
- persistence
- multi-az
