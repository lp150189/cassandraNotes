# Hinted Handoff

1. A Recovery mechnism for writes tareting offline nodes
2. Coordinator can store a hinted handoff if target node for a write 
	* is known to be down 
	* fails to acknowledge
3. Coordinator stores the hint in its system.hints table
4. when the failed node comes back online, cassandra will use system.hints to replay all the write
5. Hinted handoff comprised of 
	* address of target node which is down
	* partition and data requiring to replay
