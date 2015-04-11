# CCM- Cassandra Cluster Manager

1) What is the Cassandra Cluster Manager (CCM)?
	* create and manages multi-node clusters on a local machine
	* Useful for configuring development and test clusters
	* communicates with localhost only	
	* not used for configuring production cluster
	* meta-tool to control other tool

2) CCM may target a cluster or its nodes
	* one cluster always the current default for cluster commands
		* `ccm [cluster command] [options]`
	* nodes are automatically named node1, node2, node3, etc...
		* `ccm [nodename] [nodecommand] [options]`
	* ccm -help to list all commands
	* `ccm [command] -help` to list help and options for specific command

3) CREATE from ccm
	* `ccm create demo_1node -v 2.0.1 -n 1 -s -d` : create a cluster from cassandra version 2.0.1 with ONE node, -s means start immediately and -d meaning that it is in debug modear

4) **Some cool command from ccm**
	* ccm create <cluster_name> 
	* ccm populate -n <number_of_node> 
	* ccm status
	* ccm stop
	* ccm start
	* ccm node2 stop
	* ccm node2 start

5)Loopback interface create for cassandra to have all the host ready
```
sudo ifconfig lo0 alias 127.0.0.2 up
sudo ifconfig lo0 alias 127.0.0.3 up
sudo ifconfig lo0 alias 127.0.0.4 up
sudo ifconfig lo0 alias 127.0.0.5 up
sudo ifconfig lo0 alias 127.0.0.6 up

sudo ifconfig lo0 alias 127.0.1.1 up
sudo ifconfig lo0 alias 127.0.1.2 up
sudo ifconfig lo0 alias 127.0.1.3 up
sudo ifconfig lo0 alias 127.0.1.4 up
sudo ifconfig lo0 alias 127.0.1.5 up
sudo ifconfig lo0 alias 127.0.1.6 up
```
# We do this incase ccm start does not work
