# System Design Interview

## Aim and Goal

- To see if you got what it takes to design complex systems.
- Asses whether you can gather your thoughts in an organized manner
- Check whether you can communicate effectively and collaborate, what is your dispute resolution strategy

## During the interview

Whatever you do, don't jump straight to solution. It is a hard redflag.

### Inquiry and discovery

- Explore the requirements
- Ask questions, lots of them! Don't make assumptions.
- Learn what is important for them
- Gather the functional requirements (features. E.g: delivering live vehicle locations through an API)
- Gather the non-functional requirements (explained below heading)
- Apply paraphrase for the answers you receive, to be certain you're on the same page.
- List these requirements and features in a list and go through each of them and validate these with the interviewer. You should have a mutual agreement on each of them.

#### Questions
- Why are we building this system?
- Who are the user base, how they expect to use it?
- What is the expected user/load/request projection? What is the expected throughput. **(non-functional)**
- What regions do we expect interaction from (NA, Africa, SE Asia etc.) **(non-functional)**

#### Non-functional requirements
More seniority means more focus on non-functional requirements. 

- Security
- Consistency
- Performance
- Scalability
- Availability 
- Concurrency
- Fault-tolerance
- Freshness/caching  

### High level design

- Do not introduce irrelevant APIs or services
- Apply a top-down approach. Preferably **start from API I/O**
- You don't have to indicate any API/Communication type unless you're certain. But for example if the requirement dictates a two-way/duplex communication just design it as websocket.
- **Do not** establish any technology or protocol yet, thats for the deep-dive or low-level-design phase. In this stage you're only designing the broadview of the system. 

As for the steps to design it:
- Design the API, have agreement on I/O
- Per non-func req, put a API gateway or a Load balancer in front of the API. Don't apply it blindly.
- Put some boxes for the services, access them via API
- Put a database, don't get fancy. No need for replication, mirroring, RAID, CQRS or read-write patterns yet.
- Walk the interviewer through this broad design, make sure you're on the same page.

### Deep dive

Some common patterns to apply and consider:
#### Patterns

##### Microservices
##### Event sourcing (RabbitMQ)

##### Database Sharding
Distributing the data/database into several subsets in order to increase scalability and performance.
- Distribution/sharding logic
  - Range based: Each power of 1000s of IDs are distributed to different shards. So 0-1000 in DB1, 1001-2000 in DB2... ID, created_at, are common columns to shard by.
  - Hash-based sharding: hashing the whole data or a specific column by a hashing algorithm and distribute them by that.
  - Geo sharding: distributing the data per their origin. E.g: EU DB node, NA DB node. So a user from United States applies a query, they will be interacting with NA DB node.
- Routing to access the corresponding shard by a partition key, per sharding logic
- **It differs from database partitioning!** Partitioning is done on the same machine, while sharding has to be on different machines.

Pros:
- Faster data read
- horizontal scaling, hence scalability
- Availability. Since data is spread across different machines, it is far less likely for all of the data to be inaccessible at once opposed to single database. So at the very least, some shards are expected to be available
- Higher throughput and bandwidth

Cons:
- Complexity. It requires proper planning and maintanence.
- If done incorrectly, data loss is possible. Or some data groups might become inaccessible.
- Becomes resource-wise expensive when you have to join or query data from multiple shards.
- For most DBs, requires manual implementation. E.g: PostgreSQL doesn't have it out of the box.

##### CQRS

Command Query Responsibility Segregation. Separate read and write operations into distinct models. Applicable for systems that has disparity between read-write ratios, one of them has to weight so much more. 

##### Reverse-proxy

Gate keeping basically. Acting as a proxy for the main server/service. Receiving request and forwarding it appropriately per custom logic. Good for security, scalability, availability. 

API gateways and load balancers are famous examples.
