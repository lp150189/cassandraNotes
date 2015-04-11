# Memtable and CommitLog

1) Memtables are **in-memory representation of a CQL table**
	* Each node has a memtable for each CQL table in each keyspace
	* Each Memtable accrues writes and provide reads for data not yet flushed
2) When a Memtable flushes to disk
	1) Current Memtable data is written to a new immutable SSTable on disk. (this is a very fast sequential disk opreations)
	2) JVM heap space is reclaimed from the flushed data
	3) Corresponding CommitLog entries are marked as flushed

3) A Memtable flushes the oldes CommiLog segments to a new corresponding SSTable on disk when:
	1) memtable_total_space_in_mb is reached (default 25% of JVM heap)
	2) commitlog_total_space_in_mb is reached
	3) nodetool flush command is issued
		* `bin/nodetool flush [keyspace] [tables]`

4) Visually explaining
	1) For each write request, Node will store them **Memtable** and make a new entry to **commit log**, 
	2) Then the node will send acknowledgement back to **coordinator**
	3) When the threshold of **memtable_total_space_in_mb** or **commitlog_total_space_in_mb** reached, then **Memtables** will flush out all the segments to the **SSTable**. Also, the **CommitLog** partition got marked as flushed
	4) In the end all the **SStables** will be compacted
