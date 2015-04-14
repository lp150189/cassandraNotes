# Read request 
	
### How do read operations flow among nodes?
1) Query may read multiple partition columns
2) For each column, the coordinator returns the most recent value among all nodes recieving this particular request
3) What are eager retries?
	* if a node is slow responding to a request, the coordinator forwards it to another holding a replica of the request partition
		* New feature in 2.0+
		* RF>1

### what are the key components of the read path
1) In-Memory
	* **MemTable** in-memory tables save data as part of the merge process
	* **Row** Cache - in-memory cache stores recently read rows
	* **Bloom Filters** reports if a partition key may be in its coressponding SStable
		* report back in a request see if partition key exist in SSTable or not
	* **Key caches** maps recently read partition keys to specific SSTable offsets
	* **Partition summaries**: Sampling from partition index
2) On-disk
	* **Partition Indexes** sorted partition keys mapped to their SSTable offsets
	* **SSTable**: static files periodically flushed from each Memtables
	
	* ***MERGE***: unless served from row cache, a read uses a partition key to locate, merge and return values from a Memtable and any related SSTable storing values for that key to locate, merge, and return values from a Memtable and any related SSTable storing values for that key

3) When you send a READ request to a cluster
	* Each node( could be different depending on CL, and RF)  will send columns from each replica of each node to the coordinator
	* Then coordinator should pick the most recent one

### Read path flow
	* coordinator first hit **Row Cache**
	* if Row cache missed, then we moved on **Bloom Filter**(says maybe or yes if the key exist in SSTable)
	* **Key Cache** also saved the positive hits previously 
	* After Key cache is **Partition summary** ( subset of coressponsding indexes, let the read jump to the correct index quickly)
	* After got the **partition key** and the offset of **PK**, the partition key and its offset will be stored at **Key Cache**
	* **When all of these done , then they will be merged**
	* After all the records got merged and returned to coordinator, the records will be saved at ROW CACHE

### How is a Memtable and its SSTables used during a read?
	* Both  a MemTable and its recent SSTables are checked when reading for a partition key
		* the most current column values are merged to form the result
