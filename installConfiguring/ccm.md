# CCM- Cassandra Cluster Manager

1) What is the Cassandra Cluster Manager (CCM)?
	* create and manages multi-node clusters on a local machine
	* Useful for configuring development and test clusters
	* communicates with localhost only	
	* not used for configuring production cluster

2) CCM may target a cluster or its nodes
	* one cluster always the current default for cluster commands
		* `ccm [cluster command] [options]`
	* nodes are automatically named node1, node2, node3, etc...
		* `ccm [nodename] [nodecommand] [options]`
	* ccm -help to list all commands
	* `ccm [command] -help` to list help and options for specific command

3) CREATE from ccA
	* `ccm create demo_1node -v 2.0.1 -n 1 -s -d` : create a cluster from cassandra version 2.0.1 with ONE node, -s means start immediately and -d meaning that it is in debug modear
