Partition Process

=========================
### Partition and Tokens

1). Token: 128bit integer ID identify each partition and node

2). Partition - a unit of data storage on a node ( could be considered a row)

3). Partition key: a token calculated to identify a specific partition

4) Each node
	* Identified by the highest token in one segment of the token range
	* responsible for partitions with partitions keys in the segment before it ( primary rage)
		* in other words, each node is responsible for its primary range which is from it's location (highest token) to the previous node
	* it also could hold partition keys anywhere in the token range(secondary range)
		* Cassandra wants to know the primary range only because It uses it for the replication process, to see which replica got the data first

5) Partition keys
	* Generated by partitioners
	* Partitioner: a system on each node which hashes primary key values into a token to be used as a partition key

6) How are partitions are assigned to nodes
	* primary keys got hashed for use as partition keys
	* The data will be insert into the first replica owning the primary range

7) what is the partitioner?
	Determine where to write or read replicas
	Default Partitioner is the Murmur3Partitioner
8) Where to configure the partitioners
	* go to cassandra.yaml
	* change the partitioner to the correct one
