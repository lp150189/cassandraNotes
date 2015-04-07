1. Writes to a downed node are stored for an indefinite period as hints? **True**
2. How could you examie the properties of a CQL tables?
	* in cqlsh,  DESCRIBE TABLE <key-space-name><table-name>
3. How is the coordinator chosen for a request
	* By the client driver
4. Which of the following are functions of the partitioners?
	* Hash partition key values into tokens
	* Determine placement of first partition
5. Which of the following statements about virtual nodes are true?
	* the Num_tokens setting in cassandra.yaml is 256 vy defaule
	* Virtual Nodes minimize the impact of node failure
6. What does a consistency level determine?
	* How many nodes must acknowledge a given read or write request to the coordinator, for it to succeed
7. What is the purpose of the Snitch system?
	* to track and report cluster topology
8. Which of these statements about replication are true?
	* Subsequent replicas, beyond the first, are placed based on the replication strategy
	* The first replica is placed on the node owning the primary range of a partition's token
	* the replication factor sets how many copies to make of an original partion
9. Modifying the system keysapce can be a safe and effective approach to administering a Cassandra node. **False**
10. If a read request has a consistency level greater than ONE, the most recent column values from each node are merged into a single response . **TRUE**
11. What do all nodes share in common?
	* A clusterName
		* the answer can't be a specific replication strategy because each data center that owns multiple nodes can have different RF.
# Questions that I got wrong are
 1) **Question1**: it should be **FALSE** because hintedhandoff aslo have timeout, it doesn't last forever
 2) **Question8**:the replication factor sets how many copies to make of an original partition`
	* this is wrong because replication factor determine how many copies should be made on each data center, and if there are 3 data centers and **RF=3**, then there will be 9 copies to be made
