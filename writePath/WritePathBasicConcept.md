# Surveying basic write path concepts

1. Why cassandra write so fast?
	* **Log Structure storage engine**: Data is sequentially appended both in memory and file system, not placed in pre-set locations
	* unlike RDBMS, that seek the place where to put data, Cassandra just continously appending data
		* These continous appends will then be merged and compacted when appropriate

2. **Key components** of a write path: There are 4 elements
	* Each **node** implements four key components to handle its writes, three ***artifacts*** and one ***process***
		* ***Memtables***: in-memory tables corresponding to CQL tables, with indexes
		* ***CommitLog***: append-only log, replayed to restore downed node's Memtables
		* ***SSTables***: Memtable snapshots periodically flushed to disk, clearing heap
		* ***Compaction***: periodic process to merge and streamline ***SSTables***

3. ***Write Request Cycle*** : When any node recieve any write request (*insert, update, or delete*)
	1. The record appends to the CommitLog
	2. The record appends to the Memtable for this record's target CQL table
	3. Periodically, Memtables flush to SSTables, clearing JVM  heap and CommitLog
	4. Periodically, Compaction runs to merge and streamline SSTables

4. Notes for the **Write request cycle**
	* CommitLog and MemTable are very similar in functionality, but CommitLog is like our safety vault. When something goes wrong, and record did not get flushed to disk, we have our back-up(**Commit Log**)
	* For step 3,  when bot Memtable and CommitLog got flushed(whenever they are full) periodically to Immutable SSTables, and Memtables and CommitLog both got cleared out, commitlog will be marked at wherever it finished at.
	* In the end, **compaction** process will merge all the records from all different SSTables, and flushed to file system
