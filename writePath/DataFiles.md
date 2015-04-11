# Understanding Data Files
	
1) Data directories are created by keyspace and table names

2) Data files are created by keyspace name, table name, plus
	* format -SS table format version ('jb' is cassandra 2.0.1)
	* Generation -increment each time SSTables flush from a Memtable
	* Component -describes the type of file content
	* `<keyspace>-<table>-<format>-<generation>-<component>`
3) Each table folder contains these files
	* **Data.db** -base SSTable data include
		* row key, data size, column index , row level tombstone info, column coutn , and column list in sorted order by name
	* **Filter.db** SSTable partitions key Bloom filter, to optimize reads
	* **index.db** index for this SSTable, used for optimized reads
		* sorted row keys mapped to offsets in Data file; newer version also include column index, tombstone, and bloom filter info
	* **statistics.db** -statistic for this SSTable
		* histograms for row size and column count estimate, generation numbers of files from which this SSTable was compacted more
	* **CompressionInfo.db** metadata for Data file compression
	* **TOC.txt** component list for this SSTable
