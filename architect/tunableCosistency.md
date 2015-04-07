# Tunnable Cosistency

1. Big question when working with Cassandra is ***How consistent you want your data to be, for any given read***

2. Type of Consistency level that C* have
	* **Immediate Consistency**: read always return the most recent data
		* Consistency level **all** guarantees immediate consistency, because all replicas are read and compared before a result is returned
		* Highest latency because **all** replicas are checked and compared
	* **Eventual Consistency**: reads may return stale data
		* Consistency level **one** is very fast, because replica from the first node to respond is immediately returned, but carries the highest risk of stale data
		* Liwest latency because the first replica to reach the coordinator is returned

3. The meaing of **tune cosistency**
	* Read and write may each be set to a specific consistency level
	* ***Fomular for the immediate consistency is***
		```c++ 
		if(node_written +node_read)>replication_factor
		then immediate consistency
		```

	* We can achieve a good level of consistency by **high_read** or **high_write**
		* **high_write** consistency meaning that every node must acknowledge and update every write. With this strategy you can set the **READ CL=1** because you know that every read will have the most update data. Doing this way will make sure you have the immedate consistency by pressuring the writing side of your Cassandra.
		* **high_read** this happens if you have a very high volume of write request coming to your database, and you want to have **WRITE CL**. Then on your read side. You can set the consistency level to ***ALL** . Because Whenever are read from client comming in, the data from all ndde go compared and merged before giving back response, you will have the ***Immediate Consistency***.

4. What is the ***balance approach*** for **tune consistency**
	* ***Balanced Approach***: this approach could also achieve the **immediate consistency** 
		* There are 4 noies
		* RF =3
		* **WRITE CL = QUORUM** and **READL_CL=QUORUM**
		* Every single write or read will have at least 2 nodes acknowledge and update cassandra and leads to **immediate consistency**

5. ***Server clock synchronization***
	* Every write to any columb includes the column name, value and timestamo
	* Reads merge the most recent values from each node into one response
6. How do you chooose the consistency level.
	* is the value of immediate consistency worth the latency cost
		* Netflix actual using the CL ONE and measures the eventual consistency in milliseconds===> ***VERY GOOD***
		* ***CL=ONE*** is your fiiend .........  ***WTF***

### Important terminologies
* ***ThroughPut***: this is the numbe of transaction per second
* ***Avaiability***:  how much available data for client to use

7. ***Consistency Level Table***

|CL = ONE| CL = QUORUM| CL = ALL|
|--------|------------|---------|
|lowest latency|higher latency(than ONE)|highest latency|
|highest avaiability| lowest throughput| lowest throughput|
|highest avaiability| higher avaiability(than All)| lowest avaiability|
|stale read possible| no stale read| no stale reads|

## Question of the day: if stale is measured in milliseconds, how much are those milliseconds worth?
