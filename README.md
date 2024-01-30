# System Design
  ## Caching:
    ### Cache Replacement policies: LRU , LFU
       1) Generally LRU is being used.
       2) LFU can lead to thrashing ( that means frequent loading and evicting will happen ), because as soon as some record loads and before it's utilization if the need to load additional records, then least frequently used that means - recently loaded records will be evicted and new records will be cached.. and process can go on like that..
