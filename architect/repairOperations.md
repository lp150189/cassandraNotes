# Repair Operations

1. Inconsistencies among nodes can be repaired in multiple ways
	* ***Read repair***(read time) - automatic data partition updates during reads
	* ***Nodetool repair*** ( maintenance time) periodic full node repairs

2. Repair operations are also known as ***"Anti-entropy operations"***

3. ***Read repair***
	* read repair is done by **digest querry**
		* **digest query**: returns a hash to check the current data state, rather than return a complete result
	* After cassandra checked with the digest query and found the inconsistencies, all the node with stale data will be updated
	* ***read_repair_chance=0.1***  meaning that there are 10% chance that every read will get repair
	* ***read_repair_chance=0.1*** are associated with invidual table
	* modify property of a table by
		* ```sql
			ALTER TABLE [table] WITH [property] = [value]  
		  ```

4. ***Node tool repair***
	* `bin/nodetool -h [host] -p [JMX port] repair [options]`
	* this is a very heavy operations. There fore we should learn how to do it efficiently

5. When to run nodetool to repair
	* recover a failed node
	* bringin a downed node back online
		* if a node downed for more than something like 3 hours, run repair
	* periodically on nodes with infrequently read data
	* periodically on nodes with write or delete activity
	* periodically every gc_grace_seconds
		* ***gc_grace_seconds*** : table property controlling the tombstone garbage collection period
		* ***tombstone*** : marker palce on deleted column within a partition


