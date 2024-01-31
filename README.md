# System Design
  ## Caching:
    ### Cache Replacement policies: LRU , LFU
       1) Generally LRU is being used.
       2) LFU can lead to thrashing ( that means frequent loading and evicting will happen ), because as soon as some 
        record loads and before it's utilization if the need to load additional records, then least frequently used that means - recently loaded records 
        will be evicted and new records will be cached.. and process can go on like that..

  ## Data Replication:
    ### Pros and Cons of Primary-Replica model:
     1) Fault Tolerance           1) Consistency
     2) Improved Read Speeds      2) Write operations slower speeds (as it needs to replicated)
     ### WAL and Change Data Capture
   WAL: 
    1) Sequence of actions that happened in the DB
    2) Can be replayed multiple times and rolled back
    3) Supports txns
  Change Data Capture:
    Assume Primary database of after writing, it will put into a queue and replica will simply take that apply.
    1) This is ideal for cross-database replication.
    2) Allows transformation of data from source to destination.
      For example Cassandra is good at write operations and not reads.
      So after write operation on Cassandra by placing on queue to transform and RDS database can read transformed and copy it. So reads can happen on RDS.
    3) Can have many different type and number of subscribers/replicas.
  ### Write Amplication and Split Brain:
    Why do we need a replica db, why not both primary dbs.
    With 2 primarys, there will be split brain problem:
    Meaning there can be data inconsistency, what primary 1 has data, primary 2 can't accept the same value, it will think that what it has is correct.
    With this 
    1) Auto Reconciliation is very hard.
    2) Manual reconciliation is very slow
    The solution for this is: 
    1) Have an odd number of nodes
      otherwise with even number of nodes if there is partition in your nodes, there is possibile that half the nodes believe in some thing and another half believe in some thing else.
      But if you have odd number of nodes, even though there is split, that split can be managed in the overall majority of nodes.
   ### Write Amplification Problem:
    1) One write operation explodes into many change requests.
    2) Puts load on the primary bandwidth
    3) Choice b/w inconsistency and latency
    4) Limited writers are one solution.
    5) Cluster architecture is an alternative.
   
