# MongoDB Configuration (`mongod.conf`)

## Storage Configuration
```
storage:
  dbPath: /var/lib/mongodb  # Where MongoDB stores its data.
journal:
    enabled: true
  # engine: wiredTiger  # Specifies the storage engine.
  # wiredTiger:
  #  collectionConfig:
  #    blockCompressor: zlib  # Compress data to save space
  # engineConfig:
  #    cacheSizeGB: 2  # Limit cache to 2 GB
```
## Logging Configuration
```
systemLog:
  destination: file  # Send logs to a file
  logAppend: true  # Append new logs to the existing log file
  path: /var/log/mongodb/mongodb.log  # Path to the log file
```
## Network Configuration
```
net:
  port: 27017  # Default MongoDB port
  bindIp: 127.0.0.1,10.136.221.52,143.244.161.22  # Allow  access
```
## Process Management
```
processManagement:
  timeZoneInfo: /usr/share/zoneinfo  # Location of time zone info
```
## Security Configuration
```
security:
  authorization: enabled  # Enable user authentication
```
## Replication Configuration
```
replication:
  replSetName: "myReplicaSet"  # Replica set name
```
## Sharding Configuration
```
Sharding Configuration
sharding:
  clusterRole: "shardsvr"  # Role of this server in the sharding cluster
```
## Operation Profiling Configuration
```
operationProfiling:
  mode: slowOp  # Profile slow operations
  slowOpThresholdMs: 100  # Log operations that take more than 100 milliseconds
```
