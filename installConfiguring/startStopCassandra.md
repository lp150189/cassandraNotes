# Start and stop Cassandra Instance

1) different ways to start a cassandra instance	
	* -f start Cassandra in foreground (default is background process)
	* -p <filename>: log processID in named file, useful to stop Cassandra by PID
	* -v print the version then exit
	* -D <paramenter> pass a start up parameter
	
2) How do you locate and review log data
	* System log location is set by conf/log4j-server.properties
	* Be sure to distinguish
		* System.log: system state log, duplicates stdout, configurable by loggin level
		* CommitLog: table-specific files used during INSERT and UPDATE operations
