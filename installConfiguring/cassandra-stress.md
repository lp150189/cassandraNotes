# Cassandra-stress

1) **Definition** a command-line benchmark and load-testing ultility
	* performs inserts and reads to a test keyspace to measure performance
	* `/tools/bin/cassandra-stress`, it is not in the bin folder`
	* -o insert, read, etc
	* -t threads: process threads to use for operations
	* -k keep going: ignore errors during insert and read
	* -n num-keys: number of records to 

2) report outline of cassandra-stress
	* total: total operations since start of test
	* interval_op_rate: number of operations per second this interval
	* interval_key_rate: number of keys/rows written per second this interval
	* latency: average latency in milliseconds for each operation this interval

