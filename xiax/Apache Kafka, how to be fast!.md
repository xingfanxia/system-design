# Apache Kafka, how to be fast!
(Ref [Why Kafka Is so Fast - The Startup - Medium](https://medium.com/swlh/why-kafka-is-so-fast-bde0d987cd03))
## Modern Business-Centric Architecture
- Autonomous microservices
- Event-driven achitecture
- CQRS (command query separation)
- command - an action or
- query - return value for a query
- Creating demand for number of events a system could handle in near realtime
## Definition of *fast*

	- A multi-faceted, complex and highly ambiguous term
	- Could be latency, throughput, jitter and other metrics
	- It’s contextual
## Kafka’s fast
	- Kafka optimized for throughput at the expense of latency and jitter
	- while retaining durability, strict record order and at-least-once delivery semantics (**at-least**-**once delivery** means that for each message handed to the mechanism potentially multiple attempts are made at delivering it, such that **at least** one succeeds; again, in more casual terms this means that messages may be duplicated but not lost.)
	- so what is kafka’s fast
		- maximize throughput safely
	- Historical context:
		- Kafka born out of linkedin’s need to move terabytes of messages on a hourly basis
		- And latency wasn’t important for this kind of messaging
		- It’s `near-real-tiome` or `soft-real-time`
		- >  **Note:** For those unfamiliar with the term, ‘real-time’ does not mean ‘fast’, it means ‘predictable’. Specifically, real-time implies a hard upper bound, otherwise known as a *deadline*, on the time taken to complete an action. If the system as a whole is unable to meet this deadline each and every time, it cannot be classed as real-time. Systems that are able to perform within a probabilistic tolerance, are labelled as ‘near-real-time’. In terms of sheer throughput, real-time systems are often slower than their near-real-time or non-real-time counterparts.
## How to be fast
### low-level efficiency of the client and broker implementations
	- **Log-structured persistence**
		- It still uses disk but Kafka utilized a segmented **append-only log** limiting itself to **Sequential I/O** for both reads and writes
		- There is some misconception on **disk being slow**, it is actually not that slow for **Sequential I/O** , it is `1000 ~ 10000` times faster than **Random I/O**
		- With some advanced `read-ahead` and `write-behind` techiniques in modern OS implementations, it could be even faster with prefecthing data in large block multiples and  grouping smaller logical writes into large physical writes. Even in flash and other solid-state non-volatile media.
	- **Record batching**
		- **Sequential I/O** is blazingly fast on most media types, compared to peak performance of **network I/O** -> So if we have some clever enough design disk is able to keep up with network traffic; in fact, the bottleneck is usually **network I/O** rather than **disk I/O**
		- To improve **network I/O**, Kafka clients and brokers will accumulate multiple records in a batch, for both reading and writing, before sending them over network. This amortizes the overhead of network round-trips, using  larger packets and improving bandwidth efficiently.
	- **Batch Compression**
		- Benefits of compression is often very obvious, it is even more effective as data size increases which as discussed earlier is the case when data are processed in batch.
		- Compression ratio typically ranges from **5x to 7x**. Furthermore, record batching is largely done on the client-side, which transfer the load to clients and not only improves network bandwidth but also the broker’s disk I/O utilization.
	- **Cheaper consumers**
		- Traditional MQ-style (message queue) brokers removes messages at the point of consumption (**incuring the penalty of random I/O**).
		- Kafka, on the contrary, keep track of offsets independently at each consumer level. 
		- > The progression of offsets themselves is published on an internal Kafka topic __consumer_offsets. Again, being an append-only operation, this is fast. The contents of this topic are further reduced in the background (using Kafka’s compaction feature) to only retain the last known offsets for any given consumer group.
### Opportunistic parallelism of stream processing













