# Memtable and CommitLog

1) Memtables are **in-memory representation of a CQL table**
	* Each node has a memtable for each CQL table in each keyspace
	* Each Memtable accrues writes and provide reads for data not yet flushed
2) When a Memtable flushes to disk
	1) Current Memtable data is written to a new immutable SSTable on disk.
	2) JVM heap space is reclaimed from the flushed data
	3) Corresponding CommitLog entries are marked as flushed

3) A Memtable flushes the oldes CommiLog segments to a new corresponding SSTable on disk when:
	1) memtable_total_space_in_mb is reached (default 25% of JVM heap)
	2) commitlog_total_space_in_mb is reached
	3) nodetool flush command is issued
		* bin/nodetool flush [keyspace] [tables]
