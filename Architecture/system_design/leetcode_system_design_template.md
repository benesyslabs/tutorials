# System Design Primer #
1. [https://github.com/donnemartin/system-design-primer#how-to-approach-a-system-design-interview-question](https://github.com/donnemartin/system-design-primer#how-to-approach-a-system-design-interview-question)

# How to Approach a System Design Interview Question #
1. It is an open-ended conversation
	1. Lead it
2. Work through [System design interview questions with solutions](https://github.com/donnemartin/system-design-primer#system-design-interview-questions-with-solutions)

## Steps ##
### Step 1: Outline use cases, constraints, and assumptions ###
1. Gather requirements and scope the problem
2. Ask questions to clarify **use cases** and **constraints**
3. Discuss assumptions
4. Questions:
	1. Who is going to use it?
	2. How are they going to use it?
	3. How many users are there?
	4. What does the system do?
	5. What are the inputs and outputs of the system?
	6. How much data do we expect to handle?
	7. How many requests per second do we expect?
	8. What is the expected read to write ratio?

### Step 2: Construct a high level design ###
1. Outline high level design with all important components
	1. Sketch main components and connections
	2. Justify your ideas

### Step 3: Design core components ###
1. Dive into details for each core component
	1. Example: [design url shortening service](https://github.com/donnemartin/system-design-primer/blob/master/solutions/system_design/pastebin/README.md)
		1. Generating and storing hash of full url
			1. MD5 and Base62 (Base64 is another technique but has issues due to + and / characters)
				1. Base62 encodes to [a-zA-Z0-9] - escaping special characters is not required
				2. MD5 - 128 bit hash value (uniformly distributed)
			2. Hash collisions
			3. SQL or NoSQL
			4. Database schema
		2. Translating a hashed url to the full url
			1. Database lookup
		4. API and object-oriented design

### Step 4: Scale the design ###
1. Identify and address **bottlenecks** (given the constraints)
2. Example: Do we need the following to address scalability issues?
	1. Load balancer
	2. Horizontal scaling
	3. Caching
	4. Database sharding
3. Discuss potential solutions and **trade-offs**
	1. Everything is a trade-off
4. Address bottlenecks using [principles of scalable system design]()

### Back-of-the-envelope calculations ###
1. Might have to do some estimates by hand:
	1. Refer to [Appendix](https://github.com/donnemartin/system-design-primer#appendix)
		1. Example: How long does it take to generate 100 image thumbnails from disk
		2. Exmaple: How much memory a data structure will take
		3. Solution:
			1. Powers of Two Table:
				1. Power: Exact Value: Approx Value: Bytes
				2. 7: 128: : 
				3. 8: 256: :
				4. 10: 1024: 1 thousand: 1 KB
				5. 16: 65,536: : 64 KB
				6. 20: 1,048,576: 1 million: 1 MB
				7. 30: 1,073,741,824: 1 billion: 1 GB
				8. 32: 4,294,967,296: : 4 GB
				9. 40: 1,099,511,627,776: 1 trillion: 1 TB
			2. Latency Numbers every programmer should know
				1. Latency Comparison Numbers:
					1. L1 cache reference: 0.5 ns
					2. Branch mispredict: 5 ns
					3. L2 cache reference: 7 ns: 14 x L1 cache
					4. Mutex lock/unlock: 25 ns
					5. Main memory reference: 100 ns 20x L2 cache, 200 x L1 cache
					6. Compress 1KB with Zippy: 10,000 ns
					7. Send 1 KB over 1 Gbps network: 10,000 ns
					
## Leetcode - My System Design Template ##
### Feature Expectations (5 minutes) ###
1. Use cases
2. Scenarios that will not be covered
3. Who will use
4. How many will use
5. Usage patterns

### Estimations (5 minutes) ###
1. Throughput (QPS for read and write queries)
2. Latency expected from the system (for read and write queries)
3. Read/Write ratio
4. Traffic estimates
	- Write (QPS, Volume of data)
	- Read (QPS, Volume of data)
5. Storage estimates
6. Memory estimates
	- If we are using a cache, what is the kind of data we want to store in cache
	- How much RAM and how many machines do we need for us to achieve this?
	- Amount of data you want to store in disk/ssd

### Design Goals (5 minutes) ###
1. Latency and Throughput requirements
2. Consistency vs Availability [Weak/Strong/Eventual => consistency | Failover/replication => availability]

### High Level Design (5-10 minutes) ###
1. APIs for Read/Write scenarios for crucial components
2. Database schema
3. Basic algorithm
4. High level design for Read/Write scenario

### Deep Dive (15-20 minutes) ###
1. Scaling the algorithm
2. Scaling individual components:
	-> Availability, Consistency and Scale story for each component
	-> Consistency and availability patterns
3. Think about the following components, how they would fit in and how it would help
	1. DNS
	2. **CDN** (**Push vs Pull**)
	3. Load Balancers (**Active-Passive**, **Active-Active**, **Layer 4**, **Layer 7**)
	4. **Reverse Proxy**
	5. Application layer scaling (Microservices, **Service Discovery**)
	6. DB (RDBMS, NoSQL)
		1. RDBMS:
			1. Master-slave
			2. **Master-master**
			3. **Federation**
			4. Sharding
			5. Denormalization
			6. **SQL Tuning**
		2. NoSQL:
			1. Types:
				1. Key-Value
				2. **Wide-Column**
				3. **Graph**
				4. Document
			1. Fast-lookups
				1. RAM (Bounded size) => **Redis**, **Memcached**
				2. AP (Unbounded size) => **Cassandra**, **RIAK**, **Voldemort**
				3. CP (Unbounded size) => **HBase**, **MongoDB**, **Couchbase**, **DynamoDB**
	7. Caches
		1. Types:
			1. **Client caching**
			2. **CDN caching**
			3. **Webserver caching**
			4. **Database caching**
			5. **Application caching**
			6. **Cache @Query level**
			7. **Cache @Object level**
		2. Eviction policies:
			1. **Cache aside**
			2. **Write through**
			3. **Write behind**
			4. **Refresh ahead**
	8. Asynchronism
		1. Message queues
		2. **Task queues**
		3. **Back pressure**
	9. Communication
		1. **TCP**
		2. **UDP**
		3. REST
		4. **RPC**
	
### Justify (5 min) ###
1. Throughput of each layer
2. Latency caused between each layer
3. Overall latency justification