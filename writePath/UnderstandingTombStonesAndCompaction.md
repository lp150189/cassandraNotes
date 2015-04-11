# Tomstones and how they are used

1) What are tombstones and how they are used	
	* All writes -insert, update, or delete - append to the target Memtable
	* Deleted columns are not immediately removed, just marked
		* immediate removal would require a time-wasting seek

2) **Tombstone** a deletion marker applied to a column in its Memtable

3) **TTL** a column setting to auto-delete values after a set period
	
4) When a CQL deletes a value - a partition column - or its TTL is found to be expired during a read
	1) a tombstone (deletion marker) is applied to this column in its Memtable
	2) queries treat this column as deleted
	3) at the next Memtable flush, the tombstone passes to the new SSTable
	4) at compaction, tomstoned columns are evicted from the newly compacted SSTables
		* if older than **gc_grace_seconds**

5) What is the storage engine compaction
	* Critical, periodic SSTable maintenance process
		* merges most recent partition keys and columns
	* evicts deleted and TTL-expired partitions columns
	* create new SSTable
	* rebuild partition index and partition summary
	* delete the old SSTables
	* the process is Efficient because 
		* SSTables are inherently sorted by partition key
		* no random I/O Required
	* Necessary because
		* SSTables are immutable, so updates tend to fragment data over time
		* deletes are writes and must be periodically cleared

# Evict meaning that force updating a record inside our cql table

