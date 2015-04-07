# Virtual Nodes

1. __Definition of Virtual Node__
	* Multiple smaller segments can be owned by a node, as its primary range, instaed of one large segment
		* each smaller virutal node handles reads and writes just like a regular node
2. __Advantages of a virutal node__
	* Token rage assignment automated
	* Virtual Nodes bootstrap and decomminssion more quickly
		* **Bootstrap**: node joins cluster and fills with partitions for its primary range
			1) node join the cluster
			2) node gossips with seed nodes to learn the topology of the overall cluster
			3) fills with partition for its primary range
			4) node's tokens are automatically filled
			4) if the node doesn't exist and other nodes own the partition belongs to the new node, then other nodes would fill the new node with the partition that belongs to its range
		* **Decommission**: reverse process of a bootstrap process
			1) node leaves the cluster
			2) it drains partition to other ndoes taking responsibility for its primary range
3. __Number of token range pernode__: num_tokens in cassandra.yaml is default by 256
