# EC2 Notes

## EC2 - Elastic Compute Cloud

### Payment options

- On Demand (linux by the second, Windows by the hour)
  - No long term commitments
  - Spiky, short term work loads
  - Development use
- Reserved (1 to 3 years in length)
  - Production servers
  - Standard RI up to 75% off on-demand costs
  - Convertible RI up to 54% off on-demand costs
  - Scheduled RI runs in a reserved time window (day, week, month)
- Spot (bid a price)
  - Run a low use times
  - Need high performance for a limited time
- Dedicated Hosts (Physical servers for you)
  - Regulatory needs
  - License needs
  - Can be hourly priced
  - Up to 75% off on-demand

### Instance Types

- F1 Field Programmable Gate Array [Analytics]
- I3 High speed storage [DB]
- G3 Graphics [Video Encoding/Streaming]
- H1 High disk throughput [MapReduce]
- T2 Lowest Cost, GP [development/testing]
- D2 Dense Storage [Data Warehouse/Hadoop]
- R4 Memory optimized [Memory Intensive/DB]
- M5 GP [Application Servers]
- C5 Compute Optimized [CPU Intensive applications]
- P3 GPU [Machine Learning/Bit Coin Mining]
- X1 Memory Optimized (hugh amount of ram) [SAP/HANNA]

FightDrMcPx - remember instance types....

## EBS - Elastic Block Storage (attached volumes)

Root device volume - boot and image drive

- GP2 General Purpose SSD
  - balance of price and performance
  - 3 IOPS per GB up to 10,000 IOPS with burst up to 3000 IOPS for volumes above 3334 GB
- Pervisioned IOPS SSD
  - Database use
  - Need more than 10,000 IOPS
- ST1 Throughput optimized HDD
  - cannot be boot volume
  - log files
  - big data
    SC1 - Cold HHD
  - cannot be boot volume
    Magnetic (Std)
  - legacy
  - can boot from

## AWS CLI

- stored in ~/.aws/config ~/.aws/credentials
- aws configure --profile {profile_name}
- export AWS_PROFILE={profile_name} or setx AWS_PROFILE {profile_name}

## AWS EBS

- EBS volume must be in same availablity zone as ec2 instance.
- create encrypted root volume by copying root volume and creating an ec2 image from the copied and encrypted root volume.

## RDS

- (OLTP) SQL Server, MySQL, PostgreSQL, Oracle, Aurora, MariaDB
- (OLAP) Redshift
- Elasticache [Memcached, Redis]

### RDS Backups

- automated backups, snapshot + transaction logs
- snapshot, done manually, stored until original RDS instance is deleted.
- restored instances have a different url
- encrypted if database is encrypted,
- create an encryted database by copying a snapshot and restoring

### RDS Multi-AZ

- for disaster recovery only - synchronous replication

### RDS Read-replica

- for performance - asynchronous replication
- NOT available for Oracle or SQL Server
- 5 read replica for each DB
- can be in different availablity zone or region
- can be promoted to main DB, but breaks all read replication

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

## CloudFront

- max TTL 31536000 seconds (365 days)
- default TTL 86400 seconds (24hrs)
- protect content with signed URLs or signed cookies
- WAF projects you at the application layer, automatically projects you from
- SSL cert, can bring your own and store in ACM or IAM
