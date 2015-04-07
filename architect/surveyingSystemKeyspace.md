# Surveying the system keyspace

1. CQL command 
	* ```sql
		USE SYSTEM;
		SELECT * FROM system.schema_jeyspaces;
	  ```
2. It is not a good idea to modify the SYSTEM keyspace in cassandra

3. Keyspace tables includes

|table|Purpose|
|:----|:------|
|schema_keyspaces|Keyspaces available within this cluster, along with their assigned replication strategy and replication factor|
|schema_columns| Primary key column definitions|
|schema_columnfamilies| tables(column families_ and their configurations|
|peers| local coplies of cluster-wide gossip for this node|
|local | details of the local node's own state|
|hints| stores information of hinted handoff|



