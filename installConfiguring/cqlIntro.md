# Introduction into CQL

1) CQL stands for **Cassandra Query Language**
	* Primary interface to the Cassandra DBMS, DevCenter, native drivers
	* Modeled after Structured Query Language (SQL) for familiarity
	
2) Data definition and manipulation language(DDL and DML)

3) Familiar data types
	* blob, boolean, decimal, double, float, int, text, varchar
	* timestamp, uuid, timeuuid, counter
	* set, list, map

### No table joins for cassandra ---> query driven design

4) How to start a cql shell
	* `cqlsh [options] [host [port]]`
	* -k [keyspace] 
	* -f [filename] execute commands in file_name then exit
	* -u [username] -p [password]

5) what can cql shell do
	* support CQL DDL DML commands for schema definition and data manipulation
