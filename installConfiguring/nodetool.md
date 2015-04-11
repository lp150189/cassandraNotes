# Nodetool

1) **Definition:** A command-line cluster management utility
	* /bin/nodetool
	* `nodetool -h host -p -jmx_port [command] [options]`
		* jmx is from *cassandra-env.sh*

2) a few of the nodetool commands among 40 commands
	* status: display cluster state, load, host ID, and token
	* info: display node memory use, disk load, uptime, and similar data
	* ring: display node status and cluster ring state

3) A look at ***STATUS*** command : display summary cluster information
	* `nodetool -h [host] -p [port] status [keyspace]`
		* **U** up, **D** down
		* **N** normal, **L** leaving, **J** joining, **M** moving

4) A look at ***INFO*** command: display settings and data for specified node
	* `nodetool -h [host] -p [port] info`
	* **notes: : status and info display similar but not identical information

5) A look at ***RING*** command: displays summar state for nodes in target's node's token ring
	* `nodetool -h [host] -p [port] ring`
	* status and info provide similar data, but in greater details
	* ring aids in comparing load balance and finding downed nodes
