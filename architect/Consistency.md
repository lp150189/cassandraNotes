# Consistency Level

1. **Insert life-cycle**: Whenever an insert happen
	* Primary key got partitioned into a token
	* the first replica goes to whichever node owns the primary range for that token
	* Depending on the number of replica(RF-replication factor), and the pattern for replica(Replica Strategy) determines what nodes recieve that particular request

2. ***Consistency Level Definition***: sets how many nodes must acknowledge that request **before** a response is returned to the client

3. ***CL(Consistency level) properties***: 
	* CL is set for every request
	* By default, all request has the consistency level of one
	* CL:ONE
		* one replica node must response to any read
		* one node must response to the write request
	* client driver will determine the CL for your application
	* you can set CL in each of your request
4. ***Consistency levels that are available***
	* ALL: check all replicas node, lowest of availability
	* QUORUM: more than half
