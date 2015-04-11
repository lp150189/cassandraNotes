# Populate table in CQL
	
1) `source [filename.cql]`
	* populate keyspace and its tables this way
2) `copy [tablenames] (<column1>,<column2>,...) from [filename.csv] with header=true;`
	* copy table from external source
3) `select * from [tablename] limit 10;
	* select some records
