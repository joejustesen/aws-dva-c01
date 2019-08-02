# EC2 Notes

### EC2 - Elastic Compute Cloud

Payment options

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

Instance Types

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

### EBS - Elastic Block Storage (attached volumes)

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
