# Understanding how Memtables and SSTables operate in a read

1) How does the read path flow with **no** cached hit?
	* Row cache is going to be always checked if it is enable or not
	* **Bloom Fiter**: we have bloom filter for each of the sstables that is available
		* It determines if maybe or a yes if a pk exist in the sstable, or definitely does not
	* From the **diagram** after bloomfilter pass through **key cache**(we assume it missed), it will go to **Partition Summary**( this is there for retrieving partition key paster)
	* **Partition summary** will then point us to the **Partition Index** on our **SStables**. 
		* ***Please remember this is the first time we touch the file system***
	* After we got the **Partition Index**( which are the **offset position** of these **partitionKey** in the **SStables**), we then store these **Partition Index-offset Position**, back into the **keycache**

