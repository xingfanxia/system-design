# Spark vs Hadoop (MapReduce)
### More Memory Ops, Less Disk I/O
- More In-memory ops, minimizing unnecessary disk I/O
- Chain tasks on application level to avoid disk writes

### Advanced DAG
- Use advanced dag engine
- For every spark job, a dag of tasks is created by the engine waiting for execution
	- For `MapReduce`,  dag oly consists of two vertices, one for the map task and the other for the reduce task. And only a directed edge from the map vertex to reduce vertex.
	- For `Spark` , this dag could be very complex and highly optimized to do the least amount of work avoiding duplicate work
### Others
- Spark supports both batch and streaming yet Hadoop only batch
- Spark uses `RDD` and various storage model for fault tolerance, miming network I/O while Hadoop support fault tolerance with replicationX