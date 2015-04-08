# Commit Log

1) ***Commit Log Definition***
	* **append-only log**
	* ensure the durability of the memtable( kind of a back-up if memtable goes down)
	* If a node is restart, the commit log will be replayed to populate the memtables

2) A Memtable flushes to disk as a new SSTable when CommitLog size reaches **total allowed space**
	* ***commitlog_total_space_in_mb***: total space to be used for CommitLogs; so, size at which oldest Memtables segment flushes to SSTables
	* ***commitlog_segment_size_in_mb***: max size of invidual ***CommitLog Segment***(default:32)

3) As Memtables entries flush to SSTables, corresponding CommitLog entries are marked as flushed
	* Flushed commitLog segments are periodically recycled

4) Best practice is to locate CommitLog on its own disks to minimize write head movements, or on SSD
	* ***commitlog_director***: this should be located on a different disk, so it minimize the head movements

5) Commit Log **Entries** accrue in memory, and are synced to disk in either a batch or periodic manner
	* **commitlog_sync**: either periodic or batch(default is periodic)
	* ***Batch***: writes are not acknowledge to coordinator until the log syncs to disk
		* **commitlog_syn_batch_window_in_ms** : how long to wait for more writes before fsync
	* ***Periodic***: writes are acknowledged immediately while sync happens periodically
		* **commitlog_syn_period_in_ms**: how long to wait between fsync of log to disk (default:10000)
