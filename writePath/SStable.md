# SSTable
	
1) **SSTable**: sorted string table is
	* an immutable file of sorted partitions
	* written to dis through fast, sequential i/o
	* contains the state of a memtable when flushed

2) The current data stat of a cql table is comprised of
	* its corresponding Memtable **plus**
	* all current SSTables flushed from that **Memtable**

3) **SSTables** are periodically compacted from many to one
	
4) For each SSTable, two structure are created
	* **Partition index** list of primary keys and row start positions
	* **Partition summary** in-memory sample of partition index to speed up lookups(default: 1 of every 128)
	

5) What is ***Compaction***
	* Insert and updates mutate **Memtable** partitions, but **SSTables are immutable**
	* no SSTable seek/overwrites
	* Memtables just accrue new timestamped inserts/updates
	* ***Therefore, SSTables must be periodically compacted***
		* related SStables are merged
		* most recent version of each column is compiled to one partition in one new SSTable	
		* columns marked for delection are evicted
		* old SStables are deleted
