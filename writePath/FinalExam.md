# Final exam for write path

1) What is the default compaction strategy for a CQL table?
	* Leveled compaction

2) What causes a Memtable to flush to disk
	* the commitlog_total_sapce_in_mb threshold is reached
	* a flush command is issued by nodetool or ccm
	* a memtable_total_space_in_mb threshold is reached

3) which two process happen simultaneously for each write request?
	* Append to Memtable and Append to CommitLog

4) Which setting controls a threshold at which a Memtable will flush and create a new SSTable
	* commitlog_total_space_in_mb

5) As each SSTable is generated, the data it contains is cleared from a Memtable and marked for recycling in a CommitLog Segment
	* True
	
6) Which of the following is the best practice regarding data file and commit log directories
	* Configure each file type to use its own SSD

# Question that I got wrong

**Question 1**
	* Correct Answer: Size Tiered compaction
