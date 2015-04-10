# Cassandra Important Terminologies and Node Configuration
1) Cassandra important terminologies
	1) **Cassandra Cluster**: a peer to peer set of nodes with no single point of failure, in other words, the full set of nodes which map to a single complete token ring
	2) **Node**: one cassandra instance, in production, each node resides in a hard or virtual-box	
	3) **Partition** one unit of data on a node
		* Data structure that C\* used to control the ordering of the data
	4) **Rack**: a logical set of nodes
	5) **Data center**: a logical set of racks
		Rack and data center are organizing units for the Topology that is designed to control how your data got replicated through out the cluster

2) Key properties of cassandra.yaml
	* **cluster_name**: all nodes in a cluster must have the same value
	* **listen_address**: IP address or hostname other nodes use to connectto this node
	* **commitlog_directory**: best practices to mount on a seperate disk in production
	* **data_file_directories**: storage directory for data tables SSTables
	* **saved_caches_directory**: storages directory for key caches and row caches
	* **rpc_address/ rpc_port**: listen address/port for thrift client
	* **navtive_transport_port**: listen address for native cql driver binary protocol

3) ***Cassandra-evn.sh***
	* **JVM HEAP SETTINGS**
		* MAX_HEAP_SIZE="value"
			* Maxium recommended in production is currently 8G due to the current limiations in Java Garbage collection
		* HEAP_NEWSIZE ="value"
			* Generally set to 1/4 of MAX_HEAP_SIZE

4) ***log4j properties***
	* logging level is default as INFO, but you can also log as TRACE, DEBUG, etc.
