# Replication	

1. Target Table's keyspace determines 2 things
	* **Replication factor** : how many replicas(copies) to make for each partition
	* **Replication Strategy** : Which node should each replica be

2. **First Replica** : placed on the node owning its token's primary range
	* Based on the replication strategy(RF>1) , other replicas will be placed on other node range

3. How nodes are configured into racks and data center
	* **Rack**: a logical group of racks
	* **Data Center **: a logical group of racks

4. Replication strategy and replication factor are configured as part of declaring a new keyspace
For example:
	```sql
	CREATE KEYSPACE simple_demo WITH REPLICATION 
	{'class':'SimpleStrategy',
	 'replication_factor':2}
	```
	* Simple Strategy vs NetworkTopologyStrategy

	|Simple Strategy| NetworkTopologyStrategy|
	|---------------|------------------------|
	|one factor for entire cluster|unquie factor for each data center|
	|replication_factor:2| dc-east:2, dc-west:3|
	|create replicas on nodes subsquent to the primary rage node|based completely on racks and data centers|
	|doesn't work well with multiple data center|it is more solid and stable |

