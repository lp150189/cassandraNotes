#Internode Communications

1. ***Gossip Protocol***: continous internode communication
	* it happens every second, each node contacts 1 to the others,requestin and sharing updates about
		* Is a node available? Has it started?
		* Where is it? How is it load?
		* Is it available or bootstrapping?
	* It is used to detect failed nodes
		* failure sensitivity is also adjsutable
	* **seed node** is only used for bootstrapping process, no other purpose
	* Best pracitices for ***Gossip Protocol***

2. ***Snitch Configuration***: node sub-system to track and report cluster topology
	* inform the local partitioner about their rack and data center location
	* help enable replication without duplucation within a rack
		* duplicate replicas within a rack risk data lost if that rack fails
	* **endpoint_snitch** in cassandra.yaml controlling what type of snitch strategy you want to use
	* there are many snitch strategy available out there. You can even write your own.
