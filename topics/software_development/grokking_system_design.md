# System design

## Table of Contents
+ [References](#references)
+ [Introduction](#introduction)
  + [System design interview](#system-design-interview)
  + [Functional vs. Non-functional requirements](#functional-vs.-non-functional-requirements)
  + [Back-of-the-envelope estimations](#back-of-the-envelope-estimations)
  + [Things to avoid](#things-to-avoid)
+ [Glossary](#glossary)
  + [System design basics](#system-design-basics)
  + [Key characteristics of Distributed systems](#key-characteristics-of-distributed-systems)
  + [Load balancing](#load-balancing)
  + [Caching](#caching)
  + [Data partitioning](#data-partitioning)
  + [Indexes](#indexes)
  + [Proxies](#proxies)
  + [Redundancy and Replication](#redundancy-and-replication)
  + [SQL vs. NoSQL](#sql-vs.-nosql)
  + [CAP theorem](#cap-theorem)
  + [PACELC theorem](#pacelc-theorem)
  + [Consistent hashing](#consistent-hashing)
  + [Long-polling vs WebSockets vs Server-sent events](#long-polling-vs-websockets-vs-server-sent-events)
  + [Bloom filters](#bloom-filters)  
  + [Quorum](#quorum)
  + [Leader and follower](#leader-and-follower)
  + [Heartbeat](#heartbeat)
  + [Checksum](#checksum)  
+ [Tradeoffs](#tradeoffs)
  + [Discussing Trade-offs](#discussing-trade-offs)
  + [Strong vs Eventual Consistency](#strong-vs-eventual-consistency)
  + [Latency vs Throughput](#latency-vs-throughput)
  + [ACID vs BASE Properties in Databases](#acid-vs-base-properties-in-databases)
  + [Read-Through vs Write-Through Cache](#read-through-vs-write-through-cache)
  + [Batch Processing vs Stream Processing](#batch-processing-vs-stream-processing)
  + [Load Balancer vs API Gateway](#load-balancer-vs-api-gateway)
  + [API Gateway vs Direct Service Exposure](#api-gateway-vs-direct-service-exposure)
  + [Proxy vs Reverse Proxy](#proxy-vs-reverse-proxy)
  + [API Gateway vs Reverse Proxy](#api-gateway-vs-reverse-proxy)
  + [SQL vs NoSQL](#sql-vs-nosql)
  + [Primary-Replica vs Peer-to-Peer Replication](#primary-replica-vs-peer-to-peer-replication)
  + [Data Compression vs Data Deduplication](#data-compression-vs-data-deduplication)
  + [Server-Side Caching vs Client-Side Caching](#server-side-caching-vs-client-side-caching)
  + [REST vs RPC](#rest-vs-rpc)
  + [Polling vs Long-Polling vs WebSockets vs Webhooks](#polling-vs-long-polling-vs-websockets-vs-webhooks)
  + [CDN Usage vs Direct Server Serving](#cdn-usage-vs-direct-server-serving)
  + [Serverless Architecture vs Traditional Server-based](#serverless-architecture-vs-traditional-server-based)
  + [Stateful vs Stateless Architecture](#stateful-vs-stateless-architecture)
  + [Hybrid Cloud Storage vs All-Cloud Storage](#hybrid-cloud-storage-vs-all-cloud-storage)
  + [Token Bucket vs Leaky Bucket](#token-bucket-vs-leaky-bucket)
  + [Read Heavy vs Write Heavy System](#read-heavy-vs-write-heavy-system)
+ [Problems](#problems)
  + [System Design Interviews guide](#system-design-interviews-guide)
  + [System Design Master Template](#system-design-master-template)
  + [URL Shortening Service like TinyURL](#url-shortening-service-like-tinyurl)
  + [Pastebin](#pastebin)
  + [Instagram](#instagram)
  + [Dropbox](#dropbox)
  + [Facebook Messenger](#facebook-messenger)
  + [Twitter](#twitter)
  + [Youtube or Netflix](#youtube-or-netflix)
  + [Typeahead Suggestion](#typeahead-suggestion)
  + [API Rate Limiter](#api-rate-limiter)
  + [Twitter Search](#twitter-search)
  + [Web Crawler](#web-crawler)
  + [Facebook’s Newsfeed](#facebook-s-newsfeed)
  + [Yelp or Nearby Friends](#yelp-or-nearby-friends)
  + [Uber backend](#uber-backend)
  + [Ticketmaster](#ticketmaster)
+ [Synthesis](#synthesis)


## References

- [Grokking the system design interview](https://www.designgurus.io/course/grokking-the-system-design-interview?aff=84Y9hP)
- [Grokking the system design interview, Volume II](https://www.designgurus.io/course/grokking-system-design-interview-ii)
- [Grooking the advanced system design interview](https://www.designgurus.io/course/grokking-the-advanced-system-design-interview)
- [Grokking the modern system design interview](https://www.educative.io/courses/grokking-the-system-design-interview)
- [System design interview guide](https://www.designgurus.io/system-design-interview#basics)


## Introduction

## System design interview

**Purpose of system design interviews**: Assess a candidate's ability to design and understand complex and large-scale software systems. Assess whether you can apply engineering knowledge to real-world system architecture challenges. These questions are open-ended, there isn't a single correct answer. The emphasis is on the approach and reasoning behind the design. The goal is to evaluate how you think through large-scale problems and make engineering decisions. It's crucial for roles involving software systems and architectures (software engineer, system architect, DevOps engineer…). Key purposes are:

- __Assessing problem-solving skills__: How you approach and navigate complex, ambiguous problems. How you break them down, work towards a solution, and figure out a viable system design.
- __Evaluating technical knowledge__: Understanding of various system architecture components (databases, APIs, caching, load balancing, network protocols…), and how different pieces of a large system fit together.
- __Considering scalabitily, reliability, and maintainability__: How your design can handle growth (more user and data) and remain stable and performant over time.
- __Tradeoff analysis and decision-making__: There're many possible system designs. Why you choose a certain approach? Demonstrate great decision-making in balancing factors (performance, complexity, cost…).
- __Communication and collaboration__: Good communication is essential for explaining your design, answering questions, drawing diagrams, and collaborating with teammates.

## Functional vs. Non-functional requirements

**Functional requirements**: They describe what a system is supposed to do, the various functions that the system must perform. Examples:

- User authentication system → Validate user credentials and provide access levels.
- E-commerce website → Allow users browse products, add them to a cart, and complete purchases.
- Report generation system → Collect data, process it, and generate timely reports.

**Non-functional requirements**: They describe how the system performs a task, rather than what tasks it performs. They're related to the quality attributes of the system. Examples:

- Scalability: How it handles growth in users or data.
- Performance: How it processes transactions within a specified time.
- Availability: It should be up and running a defined percentage of time.
- Security: How it protects sensitive data and resists unauthorized access.

**Integrating both requirements**: Given an scenario, identify both the functional (what the system should do) and non-functional (how the system should do it) requirements. Balance both requirements and design a system that meets its functional goals while performing effectively, securely, and reliably. How to handle these requirements:

- __Clarify requirements__: Ask questions to understand both requirement types. Interviewers often leave these vague to see if you ask for more details.
- __Prioritize__: Identify which requirements are critical for the system's success.
- __Tradeoffs__: Discuss tradeoffs related to different architectural decisions, especially concerning functional requirements (example: a system highly optimized for read operations might have slower write operations).
- __Use real-world examples__: If you can, show practical understanding by relating your points to real-world systems or your past experiences.
- __Balance__: Don't focus too much on one type of requirement over the other. A well-rounded approach is often necessary.

## Back-of-the-envelope estimations

**Back-of-the-envelope estimations**: Technique for quickly approximating values and making rough calculations using simple arithmetic and basic assumptions. They're not detailed or exact, but help quickly grasp the scale of a system, assess the feasibility and resource needs of your solution, estimate its performance, and identify potential bottlenecks. Useful for making informed decisions and tradeoffs.

**Importance**: When designing a scalable and reliable system based on a set of requirements, the ability to make quick estimations help to:

- __Indicate system scalability__: How the system can grow or adapt.
- __Validate proposed solutions__: How you architecture meets the requirements and can handle the expected load.
- __Identify bottlenecks__: Potential performance bottlenecks and necessary adjustments to your design.
- __Demonstrate you thought process__: Shows your ability to make informed decisions and tradeoffs based on a set of assumptions and constraints.
- __Communicate effectively__ your design choices and their implications.
- __Quick decision making__: Ability to make swift estimations to guide your design decisions.

**Estimation techniques**:

- **Rules of thumb**: General guidelines or principles that can be applied to make quick and reasonably accurate estimations. They're based on experience and observations, and while not always precise, they can provide valuable insights in the absence of detailed information. Example: estimating that a user generates 1 MB of data per day on a platform can serve for basic capacity planning.

- **Approximation**: Simplifying complex calculations by rounding numbers or using easier-to-compute values. It helps derive rough estimates quickly with minimal effort. Example: assuming 1000 users instead of 1024 when estimating storage requirements can simplify calculations.

- **Breakdown and aggregation**: Breaking down a problem into smaller components and estimating each separately can make it easier to derive an overall estimate. This involves identifying the system's key components, estimating their individual requirements, and aggregating these estimates to determine the total system requirements. Example: estimating the storage needs for user data, multimedia content, and metadata separately can help in determining the overall storage requirements.

- **Sanity check**: Quick evaluation of an estimate to ensure its plausibility and reasonableness. This helps identify potential errors or oversights in the estimation process and can lead to more accurate and reliable results. Example: comparing the estimated storage requirements for a messaging service with the actual storage used by a similar existing service can help validate the estimate.

**Types of estimations** in system design:

- __Load__: Expected number of requests per second, data volume, or user traffic for the system.
- __Storage__: Amount of storage required to handle the data generated by the system.
- __Bandwidth__: Determine the network bandwidth needed to support the expected traffic and data transfer.
- __Latency__: Response time and latency of the system based on its architecture and components.
- __Resource__: Number of servers, CPUs, or memory required to handle the load and maintain desired performance levels.

**Process**:

- __Understand the scope__: Clarify the scale of the problem (how many users, how much data, …).
- __Use simple math__: Use basic arithmetic to estimate the scale of data and resources.
- __Round numbers for simplicity__: Use round numbers to make calculations easier and faster.
- __Be logical and reasonable__: Ensure your estimations make sense given the context of the problem.

**Estimation examples**:

- __Load__: A social media platform has 100 million users/day, and an average of 10 posts/user/day. Estimate load: `(100,000,000 · 10) / 86,400 seconds/day ≈ 11,574 requests/second`.
- __Storage__: A photo-sharing app has 500 million users, and an average of 2 photos uploaded by user per day, each photo with an average size of 2 MB. Estimate storage required for one day's worth of photos: `500,000,000 · 2 · 2 = 2,000,000 MB/day`.
- __Bandwidth__: A video streaming service has 10 million users streaming 1080p videos at 4 Mbps. Estimate required bandwidth: `10,000,000 · 4 = 40,000,000 Mbps`.
- __Latency__: An API fetches data from source A, B, and C, with an average latency for each source of 50 ms, 100 ms, and 200 ms, respectively. Estimate total latency: `50 + 100 + 200 = 350 ms`. If the data fetching process is parallel, the total latency is the maximum latency among the sources: `max(50, 100, 200) = 200 ms`.
- __Resource__: A web application receives 10,000 request/second, each one requiring 10 ms of CPU time. Estimate total CPU time/second: `10,000 · 10 = 100,000 ms/second`. Estimate number of required CPUs, assuming each CPU core can handle 1,000 ms of processing per second: `100,000 / 1000 = 100 cores`.

**System design examples**: Estimate the system requirements for the following design examples. By breaking down the problem into smaller components, applying estimation techniques, and aggregating the individual estimates, you can derive a rough idea of the system's requirements, which can guide your design choices and resource allocation.

- **Messaging service** (similar to WhatsApp):
  
  - __Total number of users__: Based on market research, competitor analysis, or historical data.
  - __Messages per user per day__: Average. Based on user behavior patterns or industry benchmarks.
  - __Message size__: Average. Consider text, images, videos, and other media content.
  - __Storage requirements__: Total storage needed to store messages for a specified retention period. Consider number of users, messages per user, message size, and data redundancy.
  - __Bandwidth requirements__: Bandwidth needed to handle the message traffic between users. Consider number of users, messages per user, and message size.

- **Video streaming platform** (similar to Netflix): 

  - __Total number of users__: Based on market research, competitor analysis, or historical data.
  - __Concurrent user__: Number of users streaming videos simultaneously during peak hours.
  - __Video size and bit-rate__: Average. Consider various resolutions and encoding formats.
  - __Storage requirements__: For storing the video content. Consider number of videos, their sizes, and data redundancy.
  - __Bandwidth requirements__: For handling the video streaming traffic. Consider number of concurrent users, video bit-rates, and user locations.

**Tips for estimations**:

- __Break down the problem__: Identifying the key components and estimating their requirements separately, you can aggregate your estimates to get a comprehensive view of the system needs, and even understand better how components interact with each other.
- __Use reasonable assumptions__: If you don't have all the necessary information, you can make reasonable assumptions based on your knowledge of similar systems, industry standards, or user behavior patterns.
- __Leverage your experience__: If you have experience with similar systems or certain technologies, use that knowledge to inform your estimations. 
- __Be prepared to adjust your estimations__: As the interview progresses, the interviewer may provide additional information or challenge your assumptions, requiring to adjust your estimations.
- __Ask clarifying questions__: Don't hesitate to do it if you're unsure about a requirement or assumption.
- __Communicate your thoughts__: While estimating, communicate your thought process clearly. Explain how you got your estimation and the assumptions you made.

## Things to avoid

A system design interview is not just about getting the right answer, but about demonstrating your problem-solving approach, ability to adapt, and communication and collaboration skills.

- **Don't ignore the requirements**
  - Ask questions and clarify requirements to avoid wrong designs.
  - Don't oversimplify the problem or ignore the complexities involved.
- **Don't dive into details too soon**
  - Establish high-level design before starting with low-level details.
  - Focus first on the overall architecture and how different components interact.
- **Don't stick rigidly to one idea**
  - Avoid being too rigid with your initial idea. Consider better alternatives.
  - Don't ignore the hints or feedback provided by the interviewer (sign of lack of collaboration or adaptability).
- **Don't overlook tradeoffs**
  - Every design decision has tradeoffs. Discuss them to show your deep understanding.
  - Justify decision. Explain why you chose one approach over another.
- **Don't neglect non-functional requirements**
  - Don't focus solely on functional aspects, but also on non-functional requirements (scalability, reliability…).
  - Consider real-world constraints (cost, time, existing technology…).
- **Don't under-communicate**
  - Clearly articulate your thoughts to show your understanding and approach.
  - Engage with the interviewer, ask questions, be receptive to feedback.
- **Don't be overconfident or arrogant**
  - Over-confidence may lead to dismissing valuable feedback or overlooking key aspects of the problem.
  - It's ok not to know everything. Be open about what you're unsure of to prevent providing incorrect information.


## Glossary

## System design basics

When designing a large system, we need to consider:

- What are the different architectural pieces that can be used?
- How do these pieces work with each other?
- How can we best utilize these pieces? What are the right tradeoffs?

Investing in scaling before it's needed is generally not a smart business proposition. However, some forethought into the design can save valuable time and resources in the future.

## Key characteristics of Distributed systems

Key characteristics of a distributed system include: Scalability, Reliability, Availability, Efficiency, and Manageability.

### Scalability

Capacity of a system/process/network to grow and manage increased demand. An scalable system can continuously evolve in order to support a growing amount of work. A system would like to achieve scaling without performance loss.

- There're many __reasons for scaling a system__: Increased data volume, increased amount of work (like number of transactions), etc.
- Generally, the __performance__ of a system, although designed to be scalable, declines with the system size due to the management or environment cost (example: network speed become slower because machines tend to be far apart from one another). Some tasks may not be distributed, due to their inherent atomic nature or to some flaw in the system design. At some point, such tasks would limit the speed-up obtained by distribution. A scalable architecture avoids this situation and attempts to balance the load on all the participating nodes evenly.
- __Scaling types__:
  - __Horizontal__: Scaling by adding more servers into your pool of resources. This is often easier for scaling dynamically. Examples: MongoDB, Cassandra.
  - __Vertical__: Scaling by adding more power (CPU, RAM, storage, …) to an existing server. This is usually limited by the capacity of a single server, and scaling beyond that capacity often involves downtime and comes with an upper limit. Example: MySQL.
  
![Scalability](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_1.png)

### Reliability

Ability of a system to continue operating correctly and effectively in the presence of faults, errors, or failures. A reliable distributed system keeps delivering its services even when some software or hardware components fail, and any failing machine can always be replaced by a healthy one to ensure the completion of the task.

- __Example__: A large electronic commerce store, like Amazon, ensure that any user transaction is not canceled due to a failure of the machine running it. For instance, when the user adds items to his shopping cart, the system ensures that they are not lost by implementing redundancy of both software components and data (if the server fails, another one with a replica of the shopping cart replaces it). 
- Redundancy has a __cost__.
- __Reliability__ focuses on end-to-end correctness and consistency of the entire system's operation over time. It's primarily a user-centric concept (can the system consistently meet the user's expectations over time?). It' often measured in terms of _uptime_, _error rates_, _mean time between failures_ (MTBF).
- __Fault tolerance__: System's ability to continue operating (possibly at a reduced level) even when one or more of its components fail. It allows a system to absorb or recover from faults without total breakdown. It's more of a system-centric concept (how does the system handle internal failures or component breakdowns?). It's often measured by how quickly and effective the system detects, isolates and recovers from failures (like failover times).

### Availability

Percentage of time a system/service/machine remains operational to perform its required function in a specific period, under normal conditions.

- __Example__: An aircraft with high availability can fly for many hours a month without much downtime. Availability takes into account maintainability, repair time, spares availability, and other logistics considerations. When it's down for maintenance, it's not available during that time.
- __Reliability__ is availability over time considering the full range of possible real-world conditions that can occur. An aircraft that can fly safely through any weather is more reliable than one with vulnerabilities to some conditions.
- A __reliable__ system is __available__ (high reliability contributes to high availability). But being available doesn't necessarily mean it's reliable. We can achieve high availability with an unreliable product by minimizing repair time and ensuring spares are always available when needed. Example: an online retail store has full availability for the first 2 years after launch, but the system was launched with no information security testing so, though customers are happy, the system isn't very reliable since it has serious vulnerabilities. The 3rd year the system experiences some information security incidents that cause extremely low availability for extended periods of time, resulting in reputational and financial damage to the customers.

### Efficiency

Ability of producing desired results with little resources (time or materials). Assume we have an operation that runs in a distributed manner and delivers a set of items as a result. Two standard measures of its efficiency are:

- Response time (or latency): Delay to obtain the first item.
- Throughput (or bandwidth): Number of items delivered in a given time unit (second).

These correspond to two unit costs:

- Number of messages globally sent by the nodes of the system regardless of the message size.
- Size of messages representing the volume of data exchanges.

The complexity of operations supported by distributed data structures (like searching for a specific key in a distributed index) can be characterized as a function of one of these cost units. In general, analysing a distributed structure based on the number of messages is over-simplistic because it ignores the impact of many aspects (network topology, network load, its variation, heterogeneity of software and hardware components…). Since it's quite difficult to develop a precise cost model that accurately takes into account all these performance factors, we have to live with rough but robust estimates of the system behavior.

### Manageability or Serviceability

How easy it is to operate and maintain the system. Simplicity and speed with which a system can be repaired or maintained. The longer it takes to fix a failed system, the lower availability it has. Things to consider are: ease of diagnosing and understanding problems when they occur, ease of making updates or modifications, and how simple the system is to operate (i.e., does it routinely operate without failure/exceptions?). Early detection of faults can decrease or avoid system downtime (example: some enterprise systems automatically call a service center when a system fault happens).

## Load balancing

### Load balancer (LB)

It helps spread traffic across a cluster of servers to improve responsiveness and availability of applications, websites or databases, and keeps track of the status of all resources while distributing requests. If a server is not available, or not responding, or has high error rate, LB will stop sending traffic to it. LB typically sits between client and server, accepting incoming network and application traffic and distributing traffic across multiple backend servers using various algorithms. By balancing application requests across multiple servers, LB reduces individual server load and prevents any one application server from becoming a single point of failure, thus improving overall application availability and responsiveness.

![Load balancer](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_2.png)

Before forwarding a request to a backend server, a LB first ensures that the server they choose is actually responding appropriately to requests, and then use a pre-configured algorithm to select one from the set of healthy servers. Servers health is monitored through **health checks**: regular attempts to connect to servers to ensure that they are listening. A server that fails a health check is automatically removed from the pool, and traffic will not be forwarded to it until it responds to health checks again.

For full scalability and redundancy, we can try to balance load at each system's layer. We can add LBs at 3 places:

- Between user and web server.
- Between web servers and internal platform layer (like application servers or cache servers).
- Between internal platform layer and database.

![Load balancer positions](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_3.png)

**Benefits of load balancing:**

- Users experience faster, uninterrupted service. No need to wait for a single struggling server to finish its previous task, since requests are immediately passed on to a more readily available resource.
- Service providers experience less downtime and higher throughput. Even a full server failure won't affect the end user experience as the LB will route around it to a healthy server.
- Load balancing makes it easier for system administrators to handle incoming requests while decreasing wait time for users.
- Smart LBs provide benefits like predictive analytics that determine traffic bottlenecks before they happen. It gives an organization actionable insights, which are key to automation and can help drive business decisions.
- System administrators experience fewer failed or stressed components. Load balancing has several devices performing a little bit of work, instead of a single device performing a lot of work.

**Redundant load balancers:** The LB can be a single point of failure. To overcome this, a second LB can be connected to the first to form a cluster (one is active and the other is passive). Each LB monitors the health of the other and, if the main LB fails, the second LB takes over.

![Redundant load balancers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_4.png)

### Load balancing algorithms

The LB uses them to distribute incomming traffic and requests among multiple servers or resources. Advantages:

- Ensure efficient use of resources
- Improve performance
- Maintain high availability and reliability
- Prevent any server/resource from becoming overwhelmed
- Optimize response time, maximize throughput, and enhance user experience

Most famous load balancing algorithms:

- Round Robin (weighted or not)
- Least Connections (weighted or not)
- IP Hash
- Least Response Time
- Random
- Least Bandwidth
- Custom Load

### Round Robin

Distributes incoming requests to servers in a cyclic order. After reaching the last server, it starts again at the first.

- **Pros**:
  - Equal distribution of requests among servers
  - Easy to understand and implement
  - Useful for servers with similar capacities
- **Cons**:
  - No load awareness: All servers are treated equally regardless of their load or capacity.
  - No session affinity: Subsequent requests from the same client may be directed to different servers, which can be problematic for stateful applications.
  - Performance issues when servers have different capacities or varying workloads.
  - Predictable distribution pattern: This can be exploited by attackers that find a vulnerability in a server.
- **Use cases**:
  - Homogeneous environments: All servers have similar capacity and performance.
  - Stateless applications: Each request can be handled independently.

### Least connections

Assigns incoming requests to the server with the fewest active connections at the time of the request.

- **Pros**:
  - Load awareness: Takes into account the current load on each server.
  - Dynamic distribution: Adapts to changing traffic patterns and server loads. No single server becomes a bottleneck.
  - Efficieny when servers have varying capacities and workloads.
- **Cons**:
  - Higher complexity: Requires real-time monitoring of active connections.
  - State maintenance: Requires maintaining the state of active connections, increasing overhead.
  - Potential connection spikes: When connection durations are short, serves can experience rapid spikes in connection counts, leading to frequent rebalancing.
- **Use cases**:
  - Heterogeneous environments: Servers with different capacities and workloads.
  - Variable traffic patterns: No single server is overwhelmed.
  - Stateful applications: Active sessions are distributed more evenly.

### Weighted Round Robin (WRR)

Assigns weights to each server based on their capacity or performance, distributing incoming requests proportionally according to these weights.

- **Pros**:
  - Load distribution according to capacity: Higher capacity servers handle more requests.
  - Flexibility: Easily adjustable to accommodate changes in server capacities or addition of new servers.
  - Improved performance: Prevents overloading less powerfull servers.
- **Cons**:
  - Complexity: Determining weights can be challenging and requires accurate performance metrics.
  - Increased overhead: Managing and updating weights introduce overhead.
  - Not ideal for highly variable loads: WRR may not provide optimal load balancing as it doesn't consider real-time server load.
- **Use cases**: 
  - Heterogeneous server environments: Servers with different processing capabilities.
  - Scalable web application: Servers with varying performance characteristics.
  - Database clusters: Nodes with different processing power.
  
### Weighted Least Connections

Takes into account both the current load (active connections) and relative capacity (weight) of each server.

- **Pros**:
  - Dynamic load balancing: Adjusts to the real-time load on each server.
  - Capacity awareness: Takes into account each server's capacity.
  - Flexibility: Useful with heterogeneous servers and variable load patterns.
- **Cons**:
  - Complexity: More complex to implement.
  - State maintenance: Keeps track of both active connections and server weights, increasing overhead.
  - Weight assignment: Determining weights can be challenging and requires accurate performance metrics.
- **Use cases**:
  - Heterogeneous server environments: Servers with different processing capacities and workloads.
  - High traffic web applications: Variable traffic patterns. Ensures no single server becomes a bottleneck.
  - Database clusters: Nodes with varying performance capabilities and query loads.

### IP Hash

Assigns client requests to servers based on the client's IP address. Converts client's IP address into a hash value (using a hash function) and uses it to determine which server should handle his request. The request is handled to the server number `hash_value % num_servers`.

- **Pros**:
  - Session persistence: Requests from the same IP address are routed to the same server (good for stateful applications).
  - Simplicity: Easy to implement. No need to maintain state of connections.
  - Deterministic: Predictable and consistent routing based on IP address.
- **Cons**:
  - Uneven distribution: Not evenly distributed IP addresses may lead to uneven loaded.
  - Dynamic changes: Adding/removing server can disrupt the hash mapping, rerouting some clients to different servers.
  - Limited flexibility: Doesn't take into account current load or capacity of servers.
- **Use cases**: 
  - Stateful applications: Useful when session persistence is important (online shopping carts or user sessions).
  - Geographical distributed clients: Useful when clients are distributed across different regions but consistent routing is required.

### Least Response Time

Assigns incoming requests to the server with the lowest average response time. The LB continuously monitors response times of servers (typically, time between request sent and response received).

- **Pros**:
  - Optimized performance: Requests are handled by the fastest available server.
  - Dynamic load balancing: Continuously adjusts to changing server performance.
  - Effective resource utilization: Good use of server resources by directing traffic to those that respond quickly.
- **Cons**:
  - Complexity: Complex to implement since it requires continuous monitoring of server performance.
  - Overhead: Due to monitoring response times and dynamically adjusting the load.
  - Short-term variability: Response times can vary in the short term due to network fluctuations or transient server issues, potentially causing frequent rebalancing.
- **Use cases**:
  - Real-time applications: Where low latency and fast response times are critical (online gaming, video streaming, financial trading platforms).
  - Web services and APIs: Those needing quick responses to user requests.
  - Dynamic environments: Fluctuating loads and varying server performance.

### Random

Distributes incoming requests to servers randomly.

- **Pros**:
  - Simplicity: Easy to implement and understand. Minimal configuration.
  - No state maintenance: No need to track state or performance of servers, reducing overhead.
  - Uniform distribution over time: For uniform random selection, the load will be evenly distributed across servers over time.
- **Cons**:
  - No load awareness: Doesn't consider current load or capacity of servers.
  - Potential for imbalance: In the short term, possible uneven distribution of requests.
  - No session affinity: Subsequent requests from the same client may be directed to different servers, which can be problematic for stateful applications.
  - Reduced visibility of attack patterns: Systems that detect anomalies (like DDoS attacks) might find it slightly more difficult to identify malicious patterns.
- **Use cases**:
  - Homogeneous environments: Servers with similar capacity and performance.
  - Stateless applications: Each request can be handled independently.
  - Simple deployments: Where using more complex algorithms is not justified.

### Least Bandwidth

Distributes incoming requests to servers based on the current bandwidth usage. Each new request is routed to the server that is consuming the least amount of bandwidth at the time.

- **Pros**:
  - Dynamic load balancing: Continuously adjusts to the current network load.
  - Prevents overloading: Helps prevent any single server from being overwhelmed with too much data traffic.
  - Efficient resource utilization: Servers are used more effectively by balancing the bandwidth usage.
- **Cons**:
  - Complexity: Requires continuous monitoring of bandwidth usage.
  - Overhead: Due to monitoring bandwidth and dynamically adjusting the load.
  - Short-term variability: In the short term, bandwidth usage can fluctuate, causing frequent rebalancing.
- **Use cases**:
  - High bandwidth applications: Applications with high bandwidth usage (video streaming, file downloads, large data transfers).
  - Content Delivery Networks (CDNs): They need to balance traffic efficiently to deliver content quickly.
  - Real-time applications: Where low latency is critical.

### Custom load

You define the metrics and rules for distributing incoming traffic across a pool of servers. Determine the metrics that best represent the load or performance characteristics relevant to you application (like CPU usage, memory usage, disk I/O, application-specific metrics, or a combination of metrics) and establish rules and algorithms that use these metrics to make load balancing decisions. Monitor the metrics on each server (this may involve monitoring tools or custom scripts to collect and report the data) and use your rules to dynamically adjust the distribution of incoming requests.

- **Pros**:
  - Flexibility: Highly customizable for specific needs and performance characteristics of you application.
  - Optimized resource utilization: More efficient use of server resources.
  - Adaptability: Easily adaptable to changing conditions and requirements.
- **Cons**:
  - Complexity: More complex to implement and configure.
  - Monitoring overhead: Requires continuous monitoring of multiple metrics.
  - potential for misconfiguration: Incorrectly defined metrics or rules can affect balancing and performance.
- **Use cases**:
  - Complex applications: With complex performance characteristics and varying resource requirements.
  - Highly dynamic environments: Where workloads and server performance can change rapidly and unpredictably.
  - Custom requirements: Useful when standard load balancing algorithms don't meet the specific needs of the application.

## Caching

**Locality of reference principle:** Recently requested data is likely to be requested again. Caches take advantage of this principle.

**Cache:** High-speed storage layer that sits between the applications and the original source of the data (database, file system, remote web service…). When the application requests data, it's first checked in the cache. If the data is found in the cache, it's returned to the application; otherwise, it's retrieved from its original source, stored in the cache for future use, and returned to the application. It's used in almost every computing layer (hardware, OSs, web browsers, web applications…), with various types of data (web pages, database queries, API responses, images, videos…). Caching's goal is to reduce the number of times data needs to be fetched from its original source, resulting in faster processing and reduced latency.

Load balancing helps you scale horizontally across an ever-increasing number of servers. Caching enables you to make vastly better use of the resources you already have and makes otherwise unattainable product requirements feasible.

**Concepts:**

- __Cache__: Temporary storage location for data or computation results, typically designed for fast access and retrieval.
- __Cache hit__: When a requested data item or computation result is found in the cache.
- __Cache miss__: When a requested data item or computation result is not found in the cache and needs to be fetched form the original data source or recalculated.
- __Cache eviction__: Process of removing data from the cache, typically to make room for new data or based on a predefined cache eviction policy.
- __Cache staleness__: When data in the cache is outdated compared to the original data source.

**Types of caching:** Caching can be implemented in various ways, depending on the use case and type of data. Some common types are:

- **In-memory caching:** Stores data in the main memory of the computer, which is faster to access than disk storage. Useful for frequently accessed data that fits into memory. Commonly used for caching API responses, session data, and web page fragments. Some implementation techniques are including custom caching logic within the application code, and using a cache library (Memcached, Redis…).

- **Disk caching:** Stores data on the hard disk, which is slower than main memory but faster than retireving data from a remote source. Useful for data too large to fit in memory or for data that needs to persist between application restarts. Commonly used for caching database queries and file system data.

- **Database caching:** Stores data in the database itself, reducing the need to access external storage. Useful for data stored in a database and frequently accessed by multiple users. Some implementation techniques are database query caching and result set caching.

- **Client-side caching:** Stores frequently accessed data (images, CSS, JavaScript files…) to reduce the need of repeated requests to the server. It occurs on the client device (web browser, mobile app…). Examples: browser caching, local storage, etc.

- **Server-side caching:**: Used to store frequently accessed data, precomputed results, or intermediate processing results to improve the performance of the server. It occurs on the server (typically, web applications or other backend systems). Examples: full page caching, fragment caching, object caching, etc.

- **CDN caching:** Stores data on a distributed network of servers, reducing the latency of accessing data from remote locations. useful for data accessed from multiple locations around the world (like images, videos, and other static assets). Commonly used for content delivery networks and large-scale web applications.

- **DNS caching:** Cache used in the DNS (Domain Name System) to store results of DNS queries for a period of time. The computer (user) trying to access a website sends a DNS query to a DNS server to resolve the website's domain name to an IP address. The DNS server responds with the IP address, which the computer uses to access the website. When a DNS server receives a request for a domain name, it checks its local cache to see if it has the corresponding IP address. This reduces response time for DNS queries (no need to query other servers) and improves the overall performance of the system (reduced number of queries).

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_5.png)

**Cache invalidation:** We must ensure that the data in the cache is still correct. Otherwise, we serve out-of-date (stale) information.

- __Ensure data freshness__: When the underlying data changes (prices, names…), mark or remove the old cached data (cache invalidation). Otherwise, caches will serve outdated data and lead to inconsistencies across your application.
- __Maintain system consistency__: Large systems often have multiple caching laryers. If any layer serves old data while others serve new data, user can get conflicting information. Properly invalidating caches at each layer helps maintain a consistent view of your system's state.
- __Balance performance and accuracy__: Cache invalidation strategies (time-to-live/TTL, manual triggers, even-based invalidation…) are designed to minimize the performance cost of continuously refreshing the cache. The goal is to keep data as accurate as possible while still still getting high-speed data retrieval.
- __Reduce errors and mismatched states__: When caches go stale, you risk presenting users wrong or invalid information. Strategically invalidating caches when data changes reduces these odds.

**Cache invalidation schemes**: There are 3 main schemes that are used:

- __Write-through cache__: Data is simultaneouly written into the cache and the corresponding database (permanent storage). This allows for fast retrieval, keeps consistency between cache and storage, and ensures no data is lost during a system disruption (crash, power failure…). However, since every write operation is done twice before returning success to the client, it causes higher latency for write operations.
- __Write-around cache__: Similar to write-through cache, but data is written directly to permanent storage, bypassing the cache. This reduce the cache being flooded with write operations that will not subsequently be re-read. However, a read request for recently written data will create a "cache miss" and must be read from slower back-end storage, causing higher latency.
- __Write-back cache__: Data is written to cache alone. Writting to permanent storage is done after specified intervals or under certain conditions. This results in low-latency and high-throughput for write-intensive applications. However, since the only copy of the written data is in the cache, there's risk of data loss during a system disruption.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_6.png)

**Cache invalidation methods:** Most famous ones are:

- **Purge:** Remove cached content for a specific object, URL, or set of URLs. When a purge request is received, the cached content is immediately removed. Typically used when there's an update or change to the content and the cached version is no longer valid.
- **Refresh:** Update cached content with the latest version. When a refresh request is received, the cached content is updated with the latest version from the origin server.
- **Ban:** Invalidate cached content based on specific criteria (URL pattern, header…). When a ban request is received, any cached content matching the specified criteria is immediately removed.
- **TTL (Time-to-live) expiration:** Set a time-to-live value ofr cached content, after which the content is considered stale and must be refreshed. When a request for a content is received, the cache checks the TTL value and serves the cached content if it hasn't expired. Otherwise, it fetches the latest version from the origin server and caches it.
- **Stale-while-revalidate (SWI):** Serve stale content from cache while content is updated in the background. When a request for content is received, the cached version is immediately served, and an asynchronous request is made to the origin server to fetch the latest version of the content to update the cached version. This ensures content is served quickly, even if it's slightly outdated. Used in browsers and CDNs.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_7.png)

**Cache read strategies:** Two famous ones are:

- **Read through cache:** The cache is responsible for retrieving the data from the underlying data store when a cache miss occurs. After a cache miss, cache retrieves data from the data store, updates cache, and returns data to the application. The application requests data from the cache instead of the data store directly. It maintains consistency between cache and data store, and simplifies code. Useful when data retrieval from data store is expensive, and cache misses are relatively infrequent.

- **Read aside cache (or cache-aside, or lazy loading):** The application is responsible for retrieving data from the underlying data store when a cache miss occurs. The application first checks the cache for the requested data. If not found (cache miss), the application retrieves it from data store, updates cache, and uses the data. This provides better control over the caching process, but adds complexity to the application code. Useful when you need to ensure that a cache failure won't take down your whole system, or when you want to optimize cache usage based on specific data access patterns.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_8.png)

**Cache eviction policies:** Most common ones are:

- **FIFO (First In First Out)**: The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.
- **LIFO (Last In First Out)**: Similar to FIFO, but it evicts the block accessed most recently first.
- **LRU (Least Recently Used)**: Discard the least recently used items first.
- **MRU (Most Recently Used)**: Discards the most recently used items first.
- **LFU (Least Frequently Used)**: Discards the least often used items first.
- **RR (Random Replacement)**: Randomly selects an item and discards it to make space when necessary.

## Data partitioning

**Data partitioning:** Process of dividing a large database (DB) into smaller, more manageable parts called **partitions** or **shards**. Each partition is independent and contains a subset of the overall data. Each partition is assigned to a separate processing node, which performs operations on its data subset independently of others. Datasets are partitioned based on a certain criterion. Advantages:

- Data partitioning can improve performance and scalabitily of large-scale data processing applications, as it allows processing to be distributed across multiple nodes, minimizing data transfrer and reducing processing time.
- Distributing data across multiple nodes/servers, the workload can be balanced, and the system can handle more requests and process data more efficiently.

Most popular **partitioning schemes** for large-scale applications are:

- **Horizontal partitioning** (Sharding): Divides a database into multiple partitions (shards), with each one containing a subset of rows. Each shard is typically assigned to a different database server, allowing for parallel processing and faster query execution times. However, this can lead to unbalanced servers if the value whose range is used for partitioning isn't chosen carefully.
  - Example: Social media platform that stores user data in a database table. The user table might be partitioned horizontally based on the geographic location of users, so that users in different countries are stored in different shards. This way, when a user logs in and his data needs to be accessed, the query can be directed to the appropriate shard, minimizing the amount of data that needs to be scanned.

- **Vertical partitioning**: Splits a database table into multiple partitions (shards), with each one containing a subset of columns. This can optimize performance by reducing the amount of data to scan, especially when certain columns are accessed more frequently than others.
  - Example: E-commerce website that stores customer data in a database table. The customer table might be partitioned vertically based on the type of data (personal information in one shard, order history and payment information in another). This way, when a customer logs in and their order history needs to be accessed, the query is directed to the appropriate shard, minimizing the data to scan.

- **Hybrid partitioning**: Combines horizontal and vertical partitioning. It helps optimize performance by distributing data evenly across multiple servers, while minimizing the data to scan.
  - Example: Large e-commerce website that stores customer data in a database table. The customer table might be partitioned horizontally based on customer's geographic location, and then each shard partitioned vertically based on data type. This way, when a customer logs in and his data needs to be accessed, the query can be directed to the appropriate shard, minimizing the data to scan; and each shard can be stored on a different database server, allowing for parallel processing and faster query execution times.

![Partition schemes](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_9.png)

**Partitioning criteria**: Factors or characteristics of data that can be used to divide a large dataset into smaller partitions. Most common criteria are:

- **Key or Hash-based partitioning**: Apply a hash function to some key attributes of the entity we are storing (this yields the partition number).
  - Example: We have 100 DB servers and our ID is a number that gets incremented by one each time a new record is inserted. Here, the hash function could be `ID % 100`, which gives us the server number where we can store/read that record. This ensures uniform allocation of data among servers. However, this fixes the total number of DB servers, so adding new servers requires changing the hash function, redistributing data, and downtime for the service. A workaround for this problem is using [**consistent hashing**](#consistent-hashing).

- **List partitioning**: Each partition is assigned a list of values. Whenever we want to insert a new record, we see which partition contains our key and then store it there.
  - Example: All users living in Iceland, Norway, Sweden, Finland, or Denmark are stored in a partition fo the Nordic countries.

- **Round-robin partitioning**: With n partitions, the i tuple is assigned to partition i % n. Simple strategy that ensures uniform data distribution.

- **Composite partitioning**: Combine any of the above partitioning schemes to devise a new scheme.
  - Example: First apply a list partitioning scheme and then a hash-based one. Consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key-space to a size that can be listed.

**Common problems of data partitioning**: Operations across multiple tables/rows in the same table doesn't run on the same server. This causes extra constraints on the operations that can be performed.

- **Joins and Denormalization**: Performing joins on a database running on one server is straightforward. However, it's often not feasible to perform joins that span database partitions (cross-partition queries on a partitioned database are not feasible). They're not efficient (data has to be compiled from multiple servers). Common workaround: denormalize the database so that queries that previously required joins can be performed from a single table, though this requires to deal with denormalization's perils (like data inconsistency).

- **Referencial integrity**: Enforcing data integrity constraints (like foreign keys) in a partitioned database can be extremely difficult. Most RDBMS don't support foreign keys constraints across databases on different servers, so applications requiring referencial integrity on partitioned databases often have to enforce it in application code (this often requires applications to regularly run SQL jobs to clea up dangling references.

- **Rebalancing**: There're many reasons for changing our partition scheme:
  1. Data distribution is not uniform (example: there're a many places for a ZIP code that cannot fit into one database partition).
  2. There's a lot of load on a partition (example: too may requests are handled by the DB partition dedicated to user photos.
  - In such cases, either we have to create more DB partitions or have to rebalance existing partitions, which means the partitioning scheme changed and all existing data moved to new locations. It's extremely difficult to do this without incurring downtime. Using a scheme like directory-based partitioning does make rebalancing more palatable, but increases the complexity of the system and creates a new single point of failure (the lookup service/database).


## Indexes

Sooner or later there comes a time when a database performance is no longer satisfactory. That's when you should apply **database indexing**. Creating an index on a particular table in a database can make it faster to search through the table and find the row/s that we want. Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

Example: A library catalog is a register that contains the list of books found in library. It's organized like a database table generally with four columns: book title, writer, subject, and date of publication. There're usually 2 such catalogs: one sorted by book title and one sorted by writer name. This way, you can either look by writer or by title. These catalog are like indexes for the database of books. They provide a sorted list of data that is easily searchable by relevant information.

An index is a data structure that can be perceived as a table of contents that points us to the location where actual data lives. When we create an index on a column of a table, we store that column and a pointer to the whole row in the index.

![Database index](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_10.png)

To use indexes we must consider how users will access the data. In the case of data sets of big size (many terabytes) and small payloads (e.g., 1 KB), indexes are a necessity for optimizing data access. Finding a small payload there requires iterating over too much data in an unreasonable time. Furthermore, if that data set is spread over several physical devices, we need a way to find the correct physical location of the desired data. Indexes are the best way to do this.

An index can dramatically speed up data retrieval, but a too large index can slow down data insertion, update, and deletion. Adding rows or making updates to existing rows for a table with an active index requires writing the data and updating the index, which decreases performance. Thus, avoid adding unnecessary indexes on tables, and remove those that are no longer used. Addind indexes improve search queries. If the goal of the database is to provide a data store that is often written to and rarely read from, decreasing the performance of the more common operation (writing) is probably not worth the increase in performance of reading.

More information: [Database index](https://en.wikipedia.org/wiki/Database_index)


## Proxies

**Proxy server**: Intermediate piece of software or hardware that sits between the client and the server to facilitate traffic. Typical use cases:
- Traffic control: Routes requests to the appropriate servers. Coordinates requests from multiple servers. Clients connect to a proxy to make a request for a service like a web page, file, or connection from the server.
- Optimize request traffic: It can optimize request traffic from a sytem-wide perspective by combining the same data access requests into one request and then return the result to the user (**collapsed forwarding**). If several nodes request the same data, and it is not in cache, the proxy can consolidate these requests into one so that we will only read data from disk once.
- Logging: Log requests.
- Filter requests.
- Request transformation: By adding/removing headers, encrypting/decrypting, or compressing a resource.
- URL/Content rewriting: 
- Caching: Cache data.
- Load balancing: Distributes incoming traffic across multiple backends.

**Forward proxy**: It can hide client's identity (useful for protecting clients on your internal network). It facilitates the request for resources from other servers on behalf of clients, thus anonymizing the client from the server. Focused on outbound traffic (it governs what a group of internal users can do on the open internet).

**Reverse proxy**: It can hide server's identity (useful for protecting your servers). It retrieves resources from one or more servers on behalf of a client. These resources are returned to the client, appearing as if they originated from the proxy server itself, thus anonymizing the server. Focused on inbound traffic (it governs hwo the open internet accesses a group of internal servers). Other use cases: DDoS protection, Canary experimentation (like routing 5% of users to a new version of a site).
- Example: A client making a request to `facebook.com` gets served by a reverse proxy server, which gets the response from one of the backend servers and returns it to the client.

![Proxy servers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_11.png)


## Redundancy and Replication

[**Redundancy**](https://en.wikipedia.org/wiki/Redundancy_(engineering)): Duplication of critical components or functions of a system with the intention of increasing the reliability of the system (usually in the form of a backup or fail-safe), or to improve actual system performance. This removes the single points of failure in the system and provides backups if needed in a crisis.

- Example 1: Just having a file in a single server means that if we lose the server, we lose the file. Having a duplicate or redundant copies of the file solves this problem.
- Example 2: If we have 2 instances of a service running in production and one fails, the system can failover to the other one.

Database **replication**: Process of copying and synchronizing data from one database to one or more additional databases. This is commonly used in distributed systems where multiple copies of the same data are required to ensure data availability, fault tolerance, and scalability. It's widely used in many database management systems (DBMS), usually with a primary-replica relationship between the original and the copies. The primary server gets all the updates, which then ripple through to the replica servers. Each replica outputs a message stating that it has received the update successfully, thus allowing the sending of subsequent updates. Most typical database replication strategies:

- **Synchronous replication**: Changes made to the primary database are immediately replicated to the replica databases before the write operation is considered complete. The primary database waits for the replica databases to confirm that they have received and processed the changes before the write operation is acknowledged. This ensures data consistency across all databases and reduces the risk of data loss or inconsistency.

- **Asynchronous replication**: Changes made to the primary database are not immediately replicated to the replica databases, but are queued and replicated to the replicas at a later time. There's a delay between the write operation on the primary database and the update on the replica databases, which can result in temporary inconsistencies between databases. This makes write operations faster, and allows write operations to be completed if one or more replica DBs are unavailable (the system remains available).

- **Semi-synchronous replication**: Combination of synchronous and asynchronous replication. Changes made to the primary database are immediately replicated to at least one replica database, while other replicas may be updated asynchronously. The write operation on the primary DB is not considered complete until at least one replica DB has confirmed that is has received and processed the changes. This ensures some level of storng consistency between the primary and replica DBs, and provides improved performance compared to fully synchronous replication.

![Replication types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_12.png)


## SQL vs. NoSQL

**SQL** and **NoSQL** are two different approaches to storing and managing data, each one with its own organization method and strengths.

### SQL databases (Relational databases)

**Relational databases** are the traditional ones. They shine when you need strong consistency, structured data with defined relationships, and the ability to perform complex queries. However, they can be less flexible with changes and face challenges in scaling out horizontally. Characteristics:

- **Relational data model**: Data is organized into tables (**relations**) with rows and columns. Each table represents an **entity**, and relationships between tables are defined via **foreign-keys**. Data is **structured and schema-based**, meaning your must define the schema (table structure) in advance. Example: `Users` table and `Orders` table have a relationship (via `userID`) linking orders to the user who placed them.

- **ACID properties** (Atomicity, Consistency, Isolation, Durability): Transactions in SQL databases are reliable; either all steps of a transaction complete or none do (atomicity), and the DB remains consistent and isolated during operations, with changes durable upon completion. Useful for banking applications (transferring money should not half-complete, but must deduct from one account and add to another in one atomic action).

- **SQL** (Structured Query Language): Relational databases are manipulated using SQL, a declarative query language. You specify **what** data you want (declaration), and the DB engine figures **how** to get it. This makes SQL DBs excellent for **complex queries and analytics** because you can leverage joins, aggregations (`GROUP BY`), sorting, and filtering directly in the database. Example: You can write a query to join multiple tables and filter results in one command, and the DB's query planner and optimizer will determine the best way to execute it.

- **Examples**: MySQL, PostgreSQL, Oracle, Microsoft SQL Server.

- **Use cases**: SQL DBs are best suited for applications where data is higly structured and relationships matter. Examples: financial systems and banking (transactions and consistency are critical), e-commerce platforms (orders, customers, inventory with complex relationships), and any scenario requiring multi-row transactions or sophisticated querying across data.

### NoSQL databases (Non-relational databases)

**Non-relational databases**: Broad category. More flexible and scalable. They suit modern, large-scale applications. They shine when you need to handle big data, fast. Characteristics:

- **Flexible data models**: Doesn't require a predifined schema. They can store unstructured or semi-structured data easily, and each record (or document) can have its own unique structure. Thus, you can add new fields on the fly without a painful migration. There're different types, each optimized for a certain data model.

  - **Document databases**: Data is stored in documents (JSON, BSON, …). Each document is a self-contained record (like a JSON object), which can have nested fields. Useful for data that naturally fits a hierarchical structure (like a blog post with comments, tags, …). Examples: MongoDB, CouchDB.
  - **Key-value stores**: Simplest NoSQL form. Data is stored as a key and an associated value (string, JSON, BLOB, …). It's like a big hash table or dictionary. Very fast for simple lookups by key. Example: Redis, Amazon DynamoDB.
  - **Wide-columns stores**: This use tables, but each row can have a different set of columns. They're optimized for large-scale, distributed data storage across many commodity servers. Examples: Apache Cassandra, HBase.
  - **Graph databases**: Designed for data where relationships are central. Data is stored as nodes and edges (edges represent relationships between nodes). Excellent for traversing complex relationship graphs. Examples: Neo4j, Amazon Nepture.
  - **Other NoSQL types**: In-memory databases, time-series databases, ledger databases, etc.

- **Schema flexibility**: Due to their schema-less nature, NoSQL DBs allow you to evolve your data model easily. If you need to store new attributes, you can just start storing them (no `ALTER TABLE` meeded). This is ideal for agile development environments or use cases where the data model isn't fully known upfront or changes frequently.

- **Horizontal scalability**: They're designed to scale out horizontally across multiple servers (cluster of machines) rather than just scaling up a single server. Thus, you can handle huge volumens of data and traffic by distributing the load. Many NoSQL DBs achieve scaling through sharding (partitioning data across nodes) and replication. Example: Cassandra and DynamoDB automatically distribute data based on keys, allowing them to handle web-scale workloads across many servers.

- **BASE and Eventual consistency**: Most NoSQL databases relax some of the ACID guarantees to achieve high scalability and availability. They often follow the BASE philosophy: Basically available, Soft state, Eventual consistency. This means they might allow temporary inconsistencies (different nodes might not have the exact same data at every moment), but they aim to converge to consistency over time (eventual consistency) (see [CAP theorem](#cap-theorem)). Not all NoSQL DBs are eventually consistent, but often strict consistency is traded for performance/availability. Some NoSQL systems (like MongoDB) can be configured for strong consistency in certain operations, but the general pattern is looser consistency.

- **High performance for specific use cases**: NoSQL DBs are often optimized for high performance on specific workloads. Thus, they are great for powering real-time analytics, fast web aplications, and other scenarios where speed is more critical than perfect consistency at every moment. Examples:

  - Key-value stores (like Redis) can handle millions of reads/writes per second for simple get/set operations (often used for caching). Wide-columns stores (like Cassandra) excel at write-heavy loads (logging, time-series data). Because they avoid the overhead of joins and often store data in a denormalized way, they can retrieve related data in a single read.

- **Examples**: MongoDB (document store), Apache Cassandra (wide-column store), Amazon DynamoDB (key-value store), Redis (in-memory key-value store), CouchDB (document store), Neo4j (graph database).

- **Use cases**: NoSQL is used when we have large volumes of rapidly changing or unstructured data, or requirements for massive scale and distributed access. Examples: social media platforms (storing posts, likes, messages, acros distributed clusters), content management and user-generated content systems, IoT and real-time analytics (inserting tons of events per second), gaming and ad tech (high throughput reads/writes), and caching layers.

### Key differences

- **Schema**:

  - **SQL** DBs require a predefined schema: Tables and columns (with data types) must be designed upfront, and this schema dictates what data can go into the table. The data is relational: you often normalize data into multiple tables to avoid duplication, then use relationships (joins) to query across them. This approach enforces data integrity (e.g., you can ensure via constraints that every order has a valid user), but it's rigid (changing a schema can be a big operation involving migrations and potential downtime).

  - **NoSQL** DBs are schema-flexible (or schema-less) by design. Each record (document, key-value pair, etc.) can have its own shape (e.g., one document in a MongoDB collection can have fields that another document in the same collection doesn't). This is ideal for unstructured or semi-structured data where you might not know all fields in advance. Developers can iterate quickly, adding new fields as needed without touching a central schema definition. However, without a strict schema, ensuring data consistency and integry is pushed to the application level (be careful with what you insert, because the DB won't enforce a many rules). In practice, teams often impose implicit schemas or use ORMs (Object-Relational Mapping) that validate data, but the DB itself is forgiving about structure.

- **Data model** (data relationships):

  - **SQL** relationships (one-to-one, one-to-many, many-to-many) are first-class and enforced through foreign keys and join operations. Example: you might have separate tables for `Users` and `Posts` and join them to get a user's posts. Useful if data is highly structured and you benefit from a strict schema with clear relationships.

  - **NoSQL** relationships are usually handled differently. Many NoSQL use cases favor denormalizing data, that is, storing related data together to avoid needing joins (because cross-document joins are not natively supported or efficient in most NoSQL systems). Example: in a document store, you might store user info and their posts in a single document or use a reference and handle the join logic at the application level. Document DBs can store related info together (nested), which can simplify data retrieval at the cost of duplication. Useful if data is variable or you expect the schema to evolve, or you're dealing with hierarchical data that fits better in JSON.

- **Scalability** (Vertical vs. Horizontal): 

  - **SQL** DBs are traditionally scaled vertically (scale up), meaning that if you need to handle more load, you use a bigger machine (more CPU, more RAM, faster disk/SSDs, etc.). This has a physical and cost limit (high-end hardware is expensive and finite). SQL DBs can be scaled horizontally using techniques like sharding (partitioning the data across multiple servers) or using read replicas for distributing read traffic. However, horizontal scaling in SQL is hard and not straightforward (maintaining consistency across shards, performing joins across shards, or handling multi-shard transactions adds complexity), so companies often use a single big SQL server or a primary-replica setup, until sharding is absolutely necessary. Newer technologies and distributed SQL/NewSQL DBs (like Google Spanner, CockroachDB) are tackling these challenges. Typical SQL approach: Scale up first, then carefully scale out if you must.

  - Most **NoSQL** DBs are built with the idea of an easy horizontal scaling (scale out) by adding more commodity servers. They're designed to distribute data across nodes and handle partitioning natively (e.g., adding 5 nodes to a cluster of 10 nodes might automatically rebalance data to use the new nodes). Useful for very large datasets or applications expected to grow rapidly. Massive throughput and storage can ve achieved by clustering. Many cloud services (AWS DynamoDB, Azure Cosmos DB…) are NoSQL stores that can auto-scale behind the scenes (you just pay for more throughput or nodes). To enable scaling, some sacrifice is done (like strong consistency or join capability). Example: Cassandra can handle billions of writes per day across a distributed cluster, something a single SQL instance would struggle with. SQL is useful if your data size and traffic are moderate to high but can be handled by beefing up a single server (or a primary-replica setup), though you should plan carefully if you ever hit the ceiling and need sharding

  - **Why horizontal scaling is hard for SQL?** SQL doesn't shard as easily. Its strong consistency and relational constraints need all nodes to be in sync on transactions. Queries that need data from different shards are complex. Jois across shards either are not possible or require distributed queries that are slow. Also, ACID transactions across multiple nodes require two-phase commit or other protocols which are complex and can slow things down. SQL's design assumes a single node or a tightly coupled cluster. In contrast, NoSQL systems often don't allow multi-document transactions (or limit them) and accept eventual consistency, making it easier to partition data without strict ordering between partitions. NoSQL's shared-nothing architecture aligns with horizontal scaling. NoSQL is useful if you anticipate the need to scale massively by adding lots of servers.

  - **NewSQL**: Type of modern DBs that try to blend both: offer SQL interface and ACID transactions, but with a distributed, horizontally scalable backend (e.g., Google Spanner, CockroachDB). They often use TrueTime and consensus algorithms to maintain consistency at scale.

- **Consistency, Transactions, and the CAP theorem** (ACID vs. BASE):

  - **SQL** prioritize strong consistency. Under ACID properties, when a transaction is committed to a SQL DB, all user querying the data (assuming they're not in the middle of their own transaction isolation) will see the same, up-to-date data. This is useful for bank accounts or inventory (two people shouldn't see the same $100 as available to withdraw, or sell the last item to two buyers). SQL DBs are often categorized as CP (Consistent & Partition-tolerant) in the CAP theorem (they choose consistency over availability when partitioned. So, if a SQL DB node can't reach others, it might refuse to serve some data rather than serve possibly inconsistent info. SQL's robust handling of transactions mean you can bundle multiple operations (debit one account, credit another…) into one unit that either fully succeeds of fully fails, maintaining data integrity.

  - Many **NoSQL** DBs, especially those designed to distribute across many nodes, favor availability and partition tolerance over strong consistency. They allow eventual consistency (data updates propagate to nodes over time, and for a brief period, different clients might read different data from different replicas). They tend to follow the BASE approach (Basically Available, Soft state, Eventual consistency). This is acceptable in many scenarios (like social feeds, where a slight delay is fine), but unnaceptable in others (like a financial transaction ledger).

    - Example: If you update a user's profile picture in a globally distributed NoSQL store, it might update in the US data center immediately but take a second to update in the Europe replica. A reading in Europe in that second might get the old picture (stale data), but after a short time, consistency is achieved (eventually consistent).

  - **Transactions in NoSQL**: Traditionally, NoSQL systems either didn't support multi-document transactions or had limited transaction support. The idea was to keep things simple and fast by operating mostly on single records (which are often designed to contain all related info needed for a given operation, avoiding the need for multi-object transactions). However, many modern NoSQL DBs have added some level of transactions. Example: MongoDB added multi-document transaction support (with ACID properties) in version 4.x for scenarios that need it. Still, using transactions in NoSQL is the exception rather than the norm, and often with performance or complexity trade-offs. If your application requires a lot of complex transactions spanning multiple pieces of data, SQL has a clear edge.

  - **CAP theorem**: A distributed system can only guarantee two our of three: Consistency, Availability, Partition tolerance. SQL DBs often choose Consistency + Partition tolerance over availability (especially clustered relational DBs). They'd rather be consisten and maybe not respond (or fail) if partitions happen. NoSQL (certain types, like Dynamo-style or Cassandra) often choose Availbility + Partition tolerance over consistency, thus providing high uptime and partition resilience at the cost of sometimes returning stale data. This is not universal (though there're strongly consistent NoSQL systems and highly available SQL setups), but is a general rule.

  - **ACID vs BASE**:
    - ACID (SQL) is about absolute correctness and consistency, critical for ordered, reliable transactions (like financial or legal data). An SQL DB is safe for applications that cannot tolerate inconsistent or out-of-data data and transactions.
	- BASE (NoSQL) is about being basically available and allowing inconsistency as a trade for performance and partition tolerance, often acceptable for large-scale web systems (like showing slightly out-of-data info that soon syncs). A NoSQL DB works better if you can tolerate eventual consistency and need to prioritize uptime and distribution (like a globally distributed app that should always accept writes even if nodes are partitioned).

- **Query capabilities and performance**:

  - **SQL** has rich query capabilities (join multiple tables, filter, sort, group by, use subqueries, window functions, and perform complex analytics all within the DB query). The DB engine (optimized for decades) execute them efficiently using indexes, execution plans, etc. Useful for ad-hoc queries or heavy analytical reporting on transactional data. Complex queries can have not good performance, but a well tuned SQL DB cna ahndle quite a lot on a single machine, espeically with proper indexing.

  - **NoSQL** DBs generally don't support joins (with few exeptions or limited forms). The query languages vary: some use SQL-like query languages (e.g., Cassandra has CQL, which looks like SQL for a single table; MongoDB has a JSON-based query syntax, …), but they're typically limited to fetching data by keys or simple filters within a single collection/table. For any relationship-based query, you often have to denormalize (i.e., sotre data together) so that your query doesn't need to fetch from multiple places. Many NoSQL users design their data model starting from the query patterns (_How will I need to access this data?_) and then collocate data accordingly. This makes NoSQL blazing fast for specific queries it's design for (since all needed data might be in one document or one key lookup), but makes ad-hoc queries or new query patterns harder (e.g., if you suddenly want to find "all users who posted more than 100 comments last year", and your data wasn't designed for that, you might have to scan lots of documents or even use external processing).
  
  - **Analytics and OLAP** (Online Analytical Processing):
    - For heavy analytics (OLAP), traditionally you'd use an SQL data warehouse or at least be able to export data from your SQL DB to analytical DBs. SQL DBs integrate very well with reporting tools, BI platforms, etc., due to the ubiquity of SQL.
	- NoSQL is catching up in analytics (e.g., tools like Hive allow SQL-like querying on top of NoSQL stores, and some NoSQL have aggregation frameworks), but the maturity and tooling for analytics on SQL are far richer.

  - **Full-text search of Geospacial**: These are specialized query types. Many SQL DBs have some support (like full-text indexes in MySQL or PostGIS for geospatial in PostgreSQL). NoSQL might integrate with other tools (e.g., use Elasticsearch for text search alongside a NoSQL store). If your use case needs special queries, consider if your DB choice support them or if you need a companion system. Performance considerations:
    - For **simple queries** (like key lookups or fetching a document by ID), NoSQL can be extremely fast, especially if the data is partitioned and replicated to be local to the user's region, etc. A key-value store can often outperform a relational database for simple get/put operations because it cuts out the overhead of SQL layer and joins.
	- For **complex queries**, a single SQL query might outshine multiple NoSQL calls. For instance, to get data that's spread across tables in SQL, you do one join query. In NoSQL, you might have to do several separate lookups from different collections or do a lot of client-side filtering. This can introduce more network calls and client-side processing, which reduces performance.
	- **Indexing**: Both SQL and NoSQL DBs use indexes to speed up lookups. In SQL, you index columns; in NoSQL, you might index fields in documents (e.g., MongoDB has indexes too). Performance in both depends on good indexing for query patterns. NoSQL often encourages using the primary key (or partition key) as the main query mechanism (like how DynamDB expects you to query by primary key; anything less is a full scan unless you add secondary indexes which are limited).
	- **Write performance**: Many NoSQL systems are optimized for fast writes (e.g., Cassandra has high write throughput thanks to its log-structured storage engine and distributed nature). SQL DBs can often handle fast writes as well, but their focus on immediate consistency can introduce overhead (locking, transaction coordination). For write-heavy workload (like logging millions of events), a NoSQL store might accept writes more readily (Cassandra, DynamoDB, etc., are often used for logging and telemetry for this reason).
	- **Read performance**: It depends on the query type. For simple key-value reads, NoSQL is great. For complex reads that aggregate data, SQL shines. Caching strategies often come into play too (e.g., using Redis to cache results on SQL queries, or using a search index for complex text queries).
	- **Bottom line**: For complex querying and reporting, SQL DBs offer more power out-of-the-box. For fast reads/writes on simple access patterns at huge scale, NoSQL DBs often provide better performance (since they can distribute the load and don't have the overhead of multi-table operations). Try to match your expected query patterns to the DB's strengths.

- **Flexibility and Development speed**:

  - In **SQL**, since you have a strict schema, you typically do data modeling upfront. Think about your entities, design normalized tables, and set up constraints. This can enforce good discipline and yield an efficient design for data integrity. However, if requirements change and you need to add a new field or change structures, it often involves an `ALTER TABLE` and possibly updating existing records to have default value, etc. In a large production environment, schema changes must be done carefully to avoid downtime. This rigidity means iterating quickly can be harder. In early development or prototyping, the schema may slow you down if you need to keep changin it. However, many ORMs and migration tools exist to manage this, and some developers prefer the clarity of an enforced schema.

  - In **NoSQL**, its schemaless nature lets you develop features faster initially. If you need a new piece of data stored, just start storing it. If one record has extra fields, that's fine. This can speed up development since you don't have to perform migrations for every little change, and aligns well with agile methodologies where requirements evolve. However, if you're not careful, you might end up with messy or inconsistent data structures over time (technical debt in data modeling). Also, while NoSQL allows flexible writes, when reading you still often need to handle multiple shapes of data (e.g., some documents have field X, some don`t) (called schema-on-read: you impose structure when reading out the data, instead of on write).
  - **Ecosystem and tooling**: The SQL ecosystem is very mature. There're tons of tools for reporting, TEL (extract-transform-load), backup, monitoring, ORMs, etc. Most developers learn SQL at some point. Many frameworks seamlessly integrate with SQL DBs. NoSQL, being diverse, has varied ecoystems. Some systesm like MongoDB have a strong community and many libraries, but not many off-the-shelf tools for complex operations (like a join across collections) because that's not what it's built for. NoSQL has a learning curve, both for query patterns and understanding the specific DBs behavior (consistency quirks, etc.).
  - **Maintenance and operations**: Complexity depends on the architecture. SQL has well-established best practices, while NoSQL rapid evolution require staying updated on improvements and patterns.
    - Running a single SQL DB can be simpler than managing a cluster of many nodes.
	- NoSQL's distributed nature means ops teams must handle node failures, data replication, consistency issues, etc. Managed clud services have alleviated this (you can use DynamoDB or MongoDB Atlas and not worry about the servers), but in a self-hosted scenario, NoSQL might require more effort to maintain.
	- A sharded SQL cluster can also be quite complex to maintain.
  - **Polyglot persistence**: Modern architectures might use both SQL and NoSQL for different parts of a system.
    - Example: Use SQL for the core business data (where consistence is crucial) and NoSQL for logging or caching or user session data. This requires knowing multiple systems, but many large systems are polyglot. Use the right tool for each job.
  - **Bottom line**: NoSQL offer more flexibility and speed during development since you're less constrained by schemas, which can be advantageous in fast-moving projects or when dealing with cutting-edge use cases. SQL offers a more structured environment that can prevent mistakes (e.g., you cannot accidentally insert a malformed record that breaks assumptions) and comes with a wealth of tools and knowledge in the industry. Consider you team's expertise and the project requirements. Often, starting with SQL is safe (especially if structure is clear), and introduce NoSQL components as needs arise (like scaling out reads with a caching layer, or using a document DB for a specific feature, etc.).

### Comparison table

| Aspect             | SQL DBs (Relational) | NoSQL (Non-relational) |
|:------------------:|:--------------------:|:----------------------:|
| Data model         | Relational (tables with rows and columns). Data is normalized into structured tables with defined relationships (foreign keys).                     | Variety of models (documented, key-value, column-family, graph, etc.) Data can be nested or denormalized, stored in flexible format (JSON, etc.).                       |
| Schema             | Fixed schema (must define tables and columns up front). Each row must adhere to the schema. Changing schema requires migration.                     | Dynamic schema (flexible/optional schema). Each record can have different fields. Easy to add new fields. Application logic handles interpretation.                       |
| Scalability        | Vertical scaling (add more hardware resources to the server) is the norm. Horizontal scaling (sharding) is possible but complex to implement for consistency.                     | Horizontal scaling (add more servers) is built-in for many NoSQL systems. Designed to distribute data across nodes, making it easier to scale to large data sizes or traffic volumes.                       |
| Consistency        | Strong consistency by default. Follows ACID transactions for reliable, all-or-nothing operations. Suited for use cases requiring up-to-date data and integrity (CP in CAP theorem).                     | Often eventual consistency for distributed setups. Many follow BASE (Basically Available, Soft state, Eventual consistency) for higher availability. Some can be tuned towards strong consistency at the cost of availability (AP in CAP, leaning towards availability).                       |
| Transactions       | Robust multi-step transactions supported (commit/rollback). Ensures data integrity across multiple operations (important for financial systems, etc.).                     | Limited multi-document transaction support (varies by DB). Typically focused on single-record atomic operations. Some NoSQL (like MongoDB) added transaction support, but not as full-fledged or high-performance as SQL for complex transactions.                       |
| Query capabilities | Advanced SQL queries (`JOIN`s across tables, complex `WHERE` conditions, aggregations with `GROUP BY`, subqueries, etc.) are supported by the DB engine itself. Great for analytics and relational data exploration.                     | Limited join or complex query capabilities natively. Queries are usually simple lookups by key or simple filters on one collection. For complex queries, data often needs to be structured accordingly (denormalized), or handled in application code. Some have aggregation frameworks, but as SQL-rich.                       |
| Performance        | High performance for complex queries on moderate data sizes (leverages indexes and optimized query planners). Writes can be slower if complex transactions or constraints need checking. Vertical scaling can handle a lot, but at extreme scale might bottleneck without sharding.                     | High performance for simple queries and massive scale. Can handle high write and read throughputs by spreading load (e.g., millions of ops/sec in key-value stores). Performance on complex aggregations might require external processing or map-reduce style approaches. Low latency reads/writes achievable with in-memory or geographically distributed nodes.                       |
| Flexibility        | Rigid structure (changes are slow). Great for consistency, repeatable transactions but less adaptabel to change. Any new data requirement might need altering the schema and migration data.                     | Very flexible (can adapt to changes quickly. Supports agile development (store new kinds of data as needed). Suitable for varying or eveolving data models (e.g., user profiles with varying attributes).                       |
| Ecosystem & Tools  | Extremely mature (vast array of tools for administration, analytics (SQL works with many BI tools), ORMs, etc. Many developers skilled in SQL.                     | Still maturing. Tooling depends on specific DB (each NoSQL has its own ecosystem). Fewer universal standards (though JSON is common). Need specialized knowledge for some (Cassandra data modeling, MongoDB sharding, etc.). Improving rapidly, but expertise may be less common.                       |
| Use cases          | Best for structured, relational data, like financial systems, banking, e-commerce transactions, inventory, order management, user credentials, systems needing consistent state, and complex queries. Whenever data integrity and consistency are paramount. Also, situations where the data structure is well-understood and not likely to change often.                    | Best for large-scale or flexible data, like social media (posts, comments, likes across distributed users), real-time analytics and big data, content management with varied metadata, IoT sensor data, logs, caching user sessions, and other scenarios requiring scaling out and handling lots of unstructured or semi-structured data. Great when you need high availability across regions or have rapidly evolving schemas.                      |

### What to choose?

Choosing between SQL and NoSQL depends on your project's requirements. Neither SQL nor NoSQL are universally better, they are optimized for different things. The choice is driven by the specific needs of the application. In many cases, both can complement each other in a single system. Evaluate the trade-offs in the context of your system's unique requirements. Some guidelines are:

**Choose SQL if:**

- **Data is structured and relational**: Data fits nicely into tables with clear relationships. Example: An e-commerce application with customers, orders, products, etc., where you benefit from foreign keys and joins.
- **Consistency is critical**: You cannot tolerate even minor inconsistencies. Example: Financial transactions, inventory counts, booking systems (double booking a seat due to eventual consistency delay would be bad). SQL's ACID guarantees shine here.
- **Complex querying is needed**: You need to frequently query the data in complex ways (like joining multiple tables, doing analytics, or lots of different query patterns that aren't predetermined). SQL's flexibility in querying is very valuable in such cases.
- **Transactions are a core part of the workload**: Many multi-steps operations that must all succeed or fail together (bank transfers, order placements that involve multiple tables, etc.).
- **Long-term maintenance and Reporting**: System well-understood by engineers and analysts, with existing tools for reporting, backups, etc. SQL is a mature ecosystem.

**Choose NoSQL if:**

- **Massive scale or High throughput required**: Web-scale traffic or data volume that a single server cannot handle. NoSQL is more adept at scaling out. Example: Social network's feed, log aggregation system, or any service expecting millions of users and constant growth.
- **Flexible or Evolving data models**: Data that doesn't fit a strict schema or is constantly changing (like storing documents from different sources, user-generated content with varying fields, or rapidly adding new features that require new data attributes). NoSQL lets you adapt without migrations. Great for startup or projects where requirements aren't fully nailed down.
- **Low latency, High performance simple ops**: You mostly do simple operations but at a very high volume (like caching, session storage, or real-time analytics). NoSQL can be tuned for microsecond or millisecond read/writes by sacrificing other features. Example: Redis for caching, or Cassandra for time-series inserts.
- **Geographically distributed data**: Multi-region deployments with local read/writes in each region (to serve users around the world with low latency). Many NoSQL DBs handle replication and partitioning across data centers gracefully. Some SQL solutions do this too, but it's often easier to accomplish eventual consistency models in NoSQL for multi-region.
- **Specific data models fitting NoSQL**: Data that naturally fits a document, graph, or other NoSQL model better than a relational one. Example: a social network is more straightforward in a graph DB than in SQL tables with join tables for relationships.

**Use both:**

- **Polyglot persistence**: Using different data storage technologies for different parts of the system based on their strengths.
- Example: An online retail system might use SQL DB for transactions and inventory (for accuracy), but NoSQL DB to store user activity logs, or to power a recommendation engine that needs to sift through lots of semi-structured click data.

**Explain choices**:

- Tie the choice back to requirements: 
  - "We should use SQL DB here because we need strong consistency for financial data and the ability to do complex joins for reporting. The data model is well-defined and not likely to change often".
  - "We should use a NoSQL solution here because we expect to handle a huge volume of writes globally, and we can tolerate eventual consistency. The schema might evolve, and using a document store will let us iterate without downtime".
- Mention how you'll mitigate the downsides (show you understand the trade-offs):
  - "If we use SQL and it becomes a bottlenech, we can partition by user region to scale writes, and use caching to offload reads".
  - "If we use NoSQL and we need to do some analytics, we might export the data to a warehouse or use a separate service fro those queries."

### Hybrid approach example

Imagine a high-scale web application like a ride-sharing service (Uber-like):

- A **SQL DB** could be used for critical data (ride transactions, payments, user accounts…), things that require consistency (we don't want inconsistent payment records).
- A **NoSQL DB** (or multiple) can be used for other aspects: perhaps MongoDB or Cassandra cluster to store real-time ride location logs, driver pings, etc., which are high volume and can be eventually consistent. Or use Redis to cache surge pricing data or active drivers in an area for quick retrieval.
- Maybe use a **graph DB** to maintain the relationship network of drivers, riders, referrals, etc., if that became a complex domain.
- The system becomes polyglot (each component storing data in the way that best fits its access patterns. The trade-off is complexity in maintaining multiple systems, but it can be worth it at large scale.
- For many smaller projects, sticking to one primary DB is enough, but it's useful to know that mixing isn't uncommon.


## CAP theorem

In distributed systems, different types of failures can occur (servers can crash or fail permanently, disks can go bad resulting in data losses, network connection can be lost and make part of the system inaccessible, …).

**CAP theorem**: It's impossible for a distributed system to simultaneously provide all 3 of the following desirable properties:

- **Consistency (C)**: All nodes/users see the same data at the same time. Users can read or write from/to any node in the system and will receive the same data. It's equivalent to having a single up-to-date copy of the data.
- **Availability (A)**: The system remains accessible even if one or more nodes in the system go down. Every request received by a non-failing node in the system must result in a response. Even when severe network failures occur, every request must terminate.
- **Partition tolerance (P)**: The system continues to operate even if there're partitions in the system. Such a system can sustain any network failure that does not result in the failure of the entire network. Data is sufficiently replicated across combinations of nodes and networks to keep the system up through intermittent outages.
  - **Partition**: Communication break (or network failure) between any two nodes in the system (both nodes are up but cannot communicate with each other).

Thus, we have 3 options: C+A, C+P, A+P. However, C+A is not a coherent option, as a non-partition-tolerant system will be forced to give up either C or A in the case of a network partition. Therefore, the theorem can really be stated as: **In the presence of a network partition, a distributed system must choose either Consistency or Availability**.

DB examples:

- C+P: BigTable, HBase
- A+P: Dynamo, Cassandra, CouchDB
- C+A: RDBMS

Building a general data store requires choosing 2 of those properties. If it's consistent, all nodes should see the same set of updates in the same order. But if the network loses a partition, updates in one partition might not make it to the other partitions before a client reads from the out-of-date partition after having read from the up-to-date one. The only thing that can be done to cope with this is to stop serving requests from the out-of-data partition, but then the service is no longer 100% available.


## PACELC theorem

We cannot avoid partition in a distributed system, therefore, according to **CAP theorem**, we have to choose between consistency or availability.

- **ACID** (Atomicity, Consistency, Isolation, Durability) DBs, such as RDBMSs like MySQL, Oracle, and Microsoft SQL Server, chose consistency (refuse response if it cannot check with peers).
- **BASE** (Basically Available, Soft-state, Eventually consistent) DBs, such as NoSQL DBs like MongoDB, Cassandra, and Redis, chose availability (respond with local data without ensuring it's the latest with its peers).

CAP theorem doesn't explain the choices of a distributed system when there's no network partition (when we maintain high availability by replication). PACELC theorem solves this by extending the CAP theorem (PAC is the CAP theorem, ELC is the extension).

**PACELC theorem**: In a system that replicates data:

- if there's a partition (P), a distributed system can tradeoff between availability and consistency (A and C).
- else (E), when the system runs normally in the absence of partitions, the system can tradeoff between latency (L) and consistency (C).

Examples:

- **Dynamo** and **Cassandra** are PA/EL systems: They choose A over C when a partition occurs; otherwise, they choose lower L.
- **BigTable** and **HBase** are PC/EC systems: They always choose C, giving up A and lower L.
- **MongoDB** can be considered PA/EC (default configuration): It works in a primary/secondary configuration. In default configuration, all writes and reads are performed on the primary. As all replication is done asynchronously (from primary to secondaries), when there's a network partition in which primary is lost or becomes isolated on the minority side, there's a chance of losing data that is unreplicated to secondaries, hence there's a loss of consistency during partitions. Therefore, it chooses A when a partition occurs; otherwise, it guarantees C. Alternately, when it's configured to write on majority replicas and read from the primary, it could be categorized as PC/EC.


## Consistent hashing

### Background

When designing a scalable system, the most important aspect is defining how data will be partitioned and replicated across servers. A careful designed scheme for partitioning and replicating the data enhances the system's performance, availability, and reliability, and defines how efficiently the system will be scaled and managed.

- **Data partitioning**: Process of distributing data across a set of servers (nodes). It improves the system's scalability and performance.

- **Data replication**: Process of making multiple copies of data and storing them on different servers. It improves availability and durability of the data across the system.

**Consistent hashing** was introduced by David Karger et al. in their [1997 paper](https://dl.acm.org/doi/10.1145/258533.258660) and suggested its use in distributed caching. Later, it was adopted and enhanced to be used across many distributed systems.

### Data partitioning

There're two challenges when trying to distribute data:

- How do we know on which node a particular piece of data will be stored?
- When we add or remove nodes, how do we know what data will be moved from existing nodes to the new nodes? Additionally, how can we minimize data movement when nodes join or leave?

Hashing solution: Use a suitable hash function to map the data key to a number (`number`). Apply modulo to find the server (`number % num_servers`). Example: `key = "Texas"` → `hash(key) = 16` → `16 % num_servers = 17 % 5 = 2`.

Hashing solves the problem of finding a server for storing/retrieving data. But adding or removing a server breaks all our existing mappings because the total number of servers change, which was used to find a server. To solve this, we have to remap all the keys and move our data based on the new server count (a complete mess).

### Consistent hashing

**Consistent hashing** can be used in distributed systems to distribute data across nodes. It ensures that only a small set of keys move when servers are added or removed. It stores the data managed by a distributed system in a ring. The ring is divided into smaller, predefined ranges, and each node is assigned a range of data. The start of a range is called a **token**. Each node is assigned one token. A range starts at `token_value` and ends at `next_token_value - 1`.

Example: Consider 4 in total and a hash range [1, 100]. The number range per node is 100/4. Then, all data in range [1, 25] is stored in server 1, range [26, 50] in server 2, range [51, 75] in server 3, and range [76, 100] in server 4.

| Server  | Token | Range     |
|:-------:|:-----:|:---------:|
| 1       | 1     | [1, 25]   |
| 2       | 26    | [26, 50]  |
| 3       | 51    | [51, 75]  |
| 4       | 76    | [76, 100] |

To read or write data, the [MD5 hashing algorithm]() is applied to the key to determined within which range the data lies and hence, on which node the data will be stored.

- **MD5** (MD5 Message-Digest 5 Algorithm): Hashing function that accepts a message of any length as input and returns as output a fixed-length digest value.

Consistent hashing works well when a node is added or removed from the ring, since only the next node is affected (example: when a node is removed, the next node becomes responsible for all the keys stored on the outgoing node). However, this scheme can result in non-uniform data and load distribution. This can be solved using **Virtual nodes**.

### Virtual nodes

Adding and removing nodes in a distributed system that uses Consistent hashing is handled using virtual nodes (or Vnodes).

**Basic Consistent hashing** assigns a single token (a consecutive hash range) to each physical node. Tokens are calculated based on the number of nodes. This makes adding or replacing a node an expensive operation, as we would like to rebalance and distribute the data to all other nodes, resulting in moving a lot of data. Potential issues with a manual and fixed division of ranges:

- **Adding/removing nodes**: Results in recomputing tokens causing a significant administrative overhead for a large cluster.
- **Hotspots**: Since each node is assigned one large range, if the data is not evenly distributed, some nodes can become hotspots (a server responsible for a huge partition of data can become a bottleneck because it receives a large share of data storage and retrieval requests, which can bring the performance of the whole system down).
- **Node rebuilding**: Since each node's data might be replicated (for fault-tolerance) on a fixed number of other nodes, when we need to rebuild a node, only its replica nodes can provide the data. This puts a lot of pressure on the replica nodes and can lead to service degradation.

To handle these issues, instead of assigning a single token to a node, each physical node is assigned several smaller ranges (Vnodes) (the hash range is divided into multiple smaller ranges). Each node is responsible for many tokens (or subranges) instead of just one. Advantages of Vnodes:

- Vnodes help spread the load more evenly across the physical nodes on the cluster by dividing the hash ranges into smaller subranges, which speeds up rebalancing after **adding/removing nodes**. When adding a node, it receives many Vnodes from existing nodes to maintain a balanced cluster. When **rebuilding a node**, instead of getting data from a fixed number of replicas, many nodes participate in the rebuild process.
- Vnodes make it easier to maintain a cluster containing **heterogeneous machines** because we can assign a high number of subranges to a powerful server and a lower number to a less powerful server.
- Vnodes help assign smaller ranges to each physical node, which decreases the probability of **hotspots**.

### Data replication using Consistent hashing

To ensure **high availability** and **durability**, Consistent hashing replicates each data item on multiple N nodes in the system (N is equivalent to the replication factor).

- **Replication factor**: Number of nodes that will receive the copy of the same data. Example: if a replication factor is 2, there're 2 copies of each data item, each one on a different node.
- **Availability**: System's ability to perform its required function continuously without failing for a designated period of time.
- **Durability**: System's ability to prevent the loss of data that was successfully committed to it. Durability guarantees against any data loss due to corruption or a permanent component failure.

Each key is assigned to a **coordinator node** (generally the first node that falls in the hash range), which first stores the data locally and then replicates it to N-1 clockwise successor nodes on the ring. This results in each node owning the region of the ring between it and its Nth predecessor. In an **eventually consistent** system, this replication is done asynchronously (in the background), so copies of data don't always have to be identical as long as they are designed to eventually become consistent, which is used to achieve high availability.

### Overview

Consistent hashing helps with efficiently partitioning (scalability) and replicating data (availability). Amazon's [Dynamo](https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html) and Apache [Cassandra](https://en.wikipedia.org/wiki/Apache_Cassandra) use Consistent hashing to distributed and replicate data across nodes. Use case examples:

- System working with a set of storage (or database) servers that needs to scale up or down based on usage.
- Distributed system that needs dynamic adjustment of its cache usage by adding or removing cache servers based on the traffic load.
- System that wants to replicate its data shards to achieve high availability.


## Long-polling vs WebSockets vs Server-sent events

Long-Polling, WebSockets, and Server-Sent Events are popular **communication protocols** between a client (like a web browser) and a web server.

**HTTP protocol** (Hypertext Transfer Protocol): Application layer protocol in the Internet protocol suite. Foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources. It's a request-response protocol in the client-server model. A transaction starts with a client (like a web browser) submitting a request to a server (web server, hosting server…), which it attempts to satisfy and returns a response to the client describing the disposition of the request and optionally contains a requested resource. Standard HTTP web request:

1. A client opens a connection and requests data from the server.
2. The server calculates the response.
3. The server sends the response back to the client on the opened request.

### Ajax Polling

**AJAX** (Asynchronous JavaScript and XML): Web development technique that enables web applications to send and receive data from a server asynchronously, without requiring a full page reload. This allows for dynamic updates to specific parts of a webpage, improving responsiveness and user experience.

**Polling**: Standard technique used by most AJAX applications. The client repeatedly polls (or requests) a server for data. The client makes a request and waits for the server to respond with data. If no data is available, an empty response is returned.

- The client opens a connection and requests data from the server using regular HTTP.
- The requested webpage sends requests to the server at regular intervals (like 0.5 s).
- The server calculates the response and sends it back, just like regular HTTP traffic.
- The client repeats the above 3 steps periodically to get updates from the server.

Problem: The client has to keep asking the server for any ne data. This results in a lot of empty responses, creating HTTP overhead.

### HTTP Long-Polling

**Long-Polling** (or Hanging GET): Variation of the traditional polling. It allows the server to push data to a client whenever the data is available. The client requests data from the server like in normal polling, but expecting that the server may not respond immediately.

- If the server doesn't have any data available for the client, instead of sending an empty response, it holds the request and waits until some data becomes available.
- Once data is available, a full response is sent to the client. Then the client immediately re-requests data from the server so that the server will almost always have an available waiting request that it can use to deliver data in response to an event.

Basic life cycle of an application using HTTP Long-Polling:

1. The client makes an initial request using regular HTTP and then waits for a response.
2. The server delays its response until an update is available or a timeout has occurred.
3. When an update is available, the server sends a full response to the client.
4. The client typically sends a new long-poll request, either immediately upon receiving a response or after a pause to allow an acceptable latency period.
5. Each Long-Poll request has a timeout. The client has to reconnect periodically after the connection is closed due to timeouts.

### WebSockets

**Full-duplex (FDX)**: System allowing communication in both directions and simultaneously (unlike half-duplex). Example: telephones.

**WebSocket**: It provides [Full-duplex](https://en.wikipedia.org/wiki/Duplex_(telecommunications)#Full_duplex) communication channels over a single TCP connection. It provides a persistent connection between a client and a server that both parties can use to start sending data at any time. The client stablishes a WebSocket connection through a WebSocket handshake. If this process succeeds, then the server and client can exchange data in both directions at any time. This protocol enables communication between a client and server with lower overheads, facilitating real-time data transfer from and to the server. This is possible with a standardized way for the server to send content to the browser without being asked by the client and allowing for messages to be passed back and forth while keeping the connection open. This allows a two-way (bi-directional) ongoing conversation between client and server.

### Server-Sent Events (SSEs)

Under SSEs the client establishes a persistent and long-term connection with the server. The server uses this connection to send data to a client. If the client wants to send data to the server, it would require the use of another technology/protocol to do so.

1. Client requests data from a server using regular HTTP.
2. The requested webpage opens a connection to the server.
3. The server sends the data to the client whenever there's new information available.

SSEs are best when we need real-time traffic from the server to the client or if the server is generating data in a loop and will be sending multiple events to the client.


## Bloom filters

### Introduction

**Bloom filter**: Magical checklist that can answer questions of the form "Have we seen this item before?". It consists of 2 main components:

- **Bit array**: Array of bits, initially all set to 0.
- **Hash functions**: Several independent hash functions that each take an input item and produce and index (position in the bit array).

**Operations** on the Bloom filter:

- **Add an item**: The item is run through each hash function to get multiple array positions, and all the bits at all those positions are set to 1.
- **Query item** (check membership): The item is run through the hash functions to get the positions and check the bits.
  - If any one of those bits is 0, the item was definetely not in the set.
  - If all of those bits are 1, then the item is probably in the set (it could be a false positive).
  
Bloom filters **guarantee no false negative**. Any item added will have its bits set. But item that were never added might by coincidence have all their bits set by other items, leading the filter to erroneously report "probably present".

Using multiple hash functions spreads the influence of each item across the array. This redundancy makes false negative impossible: an item would have to lose all its bits to be missed, which can't happen unless we explicitly remove it. But if too many items crowd the same few positions, they can cause false positives by filling in all the bits for some item that wasn't added.

### How Bloom filters work

Consider 3 items (P, Q, R). Each item is hashed by 3 hash functions to specific positions in the bit array, which are then set to 1. To query a new item, you hash it and check the corresponding bit positions; if any required bit is 0, the item is definitely not in the set, but if all are 1 the item is probably in the set.

**Usage process**:

1. **Initialize**: Start with a bit array of length N, all bits set to 0. Decide on k independent hash function (each should output a number in range [0, N-1]).
2. **Adding an item**: Feed the item into each hash function to get k array indices. For each index, set the bit at that position in the array to 1.
3. **Querying a item**: Check if an element is in the set by running it through the same k hash functions to get k positions. Then check those positions in the bit array:
  - If any of those bits is 0, the item in not in the set.
  - If all k bits are 1, the item is possibly in the set. Either the item was added or those bits happened to be set by some other combination of items. There's a small chance that it's a false positive.
4. **Dealing with false positives**: If the filter answers "probably in the set", one usually double-checks via a slower method (like doing full lookup in a DB or cache) if exact confirmation is needed. The filter's job is mainly to screen out definitively missing items quickly, to avoid wasting time on costly lookups for items that aren't there.

These steps make Bloom filters extremely fast and memory-efficient. The time to add or check an item is O(k), where k is the number of hash functions (constant, independent of the number of stored elements). In practice, k is fixed and usually small (like 3 to 10), so Bloom filter operations take a fixed few hash computations and array accesses. This constant-time performance holds even when the set represented is huge (millions of items), which is a big advantage over structures like lists or trees for membership testing.

**Removing items**: Not supported in standard Bloom filters. Clearing a bit set to 1 could remove information about other items that hashed that bit. You can only add items or reset everything. Bloom filters are best suited for scenarios where the set only accumulates or where you can occasionally rebuild or refresh the filter if needed.

- There're variantes like **Counting Bloom filters** that use counters instead of single bits to allow deletions, but they use more memory and complexity.

### False positives

Bloom filters trade perfect accuracy for efficiency.

Once a bit is set to 1 for an added item, that bit remains set, ensuring no future query for that item will find a 0 and falsely conclude "not present". 

False positives happen because different items overlap in the bits they set. Sometimes, an unlucky combination of items can fill all the bits that a query item would require. The Bloom filter has no way to tell that those bits were set by other items, so it can only report "probably present". A Bloom filter compresses information about the set, which saves space, but loses the ability to distinguish some different combinations of items.

The probability of a false positive can be tuned by adjusting this:

- Size of the bit array (n): The bigger it is, the more sparsely bits are filled for the same number of items, reducing the chance of accidental overlaps.
- Number of hash functions (k): The bigger the number, the more bits are covered by each items, which can either increase or decrease false positives depending on balance (too few hashes and each item doesn't mark enough territory, too many and you fill the array too quickly).

There's an optimal k for a given n and number of items that minimizes false positives. Designers choose parameters so that false positive probability is very low (say 1% or 0.1% or even less) based on what's acceptable for the application. A clear trade-off is: more memory = fewer false positives. Many systems let you configure this trade-off (example: Apache Cassandra, a distributed DB, allows tuning the Bloom filter's target false-positive rate, using more RAM to get it as low as needed).

False positives are the price of massive space and time savings. In exchange for never missing a member and using very little memory, we accept a slim chance of getting a "maybe" for something that isn't really there. In scenarios where a false positive only causes a minor extra step (like unnecessary DB lookup), Bloom filters are a huge win.

## Quorum

In distributed systems, data is replicated across multiple servers for fault tolerance and high availability. However, how to make sure that all replicas are consistent? (i.e., that all have the latest copy of the data and all clients see the same data).

**Quorum**: Minimum number of server on which a distributed operation needs to be performed successfully before declaring the operation's success.

Consider a DB replicated on 5 machines. The quorum is the minimum number of machines that perform the same action (commit or abort) for a given transaction in order to decide the final operation for that transaction. Three machines form the majority quorum, and if they agree, we will commit that operation. Quorum enforces the consistency requirement needed for distributed operations.

In systems with multiple replicas, it's possible that users read inconsistent data (data that is behind the last update).

What value should we choose for a quorum? More than half of the number of nodes in the cluster: N/2 + 1 (where N = total number of nodes in the cluster).

- In a 5-node cluster, 3 nodes must be online to have a majority. The system can afford 2 node failures.
- In a 4-node cluster, 3 nodes must be online to have a majority. The system can afford 1 node failure.
- Thus, it's recommended to have an odd number of totla nodes in the cluster.

Quorum is achieved when nodes follow **R + W > N** (where N = nodes in the quorum group, W = minimum write nodes, R = minimum read nodes). If a distributed system follows this rule, every read will see at least one copy of the latest value written. Examples:

- N=3, W=2, R=2: Common configuration. Strong consistency.
- N=3, W=1, R=3: Fast write, slow read, not very durable.
- N=3, W=3, R=1: Slow write, fast read, durable.

Before deciding read/write quorum, keep in mind this:

- R=1, W=N: Full replication (write-all, read-one). Undesirable when servers can be unavailable because writes are not guaranteed to be complete.
- 1<R<W<N: Best performance (throughput/availability) because reads are more frequent than writes in most applications.

**How it works:**

- **Majority-based quorum**: Most common quorum type. An operation requires a majority (more than half) of the nodes to agree or participate. Example: in a system with 5 nodes, at least 3 must agree for a decision to be made.
- **Read and write quorums**: For read and write operations, different quorum sizes can be defined. Example: a system might require a write quorum of 4 nodes and a read quorum of 2 nodes in a 5-node cluster.

**Use cases:**

- **Distributed DBs**: Ensuring consistency in a DB cluster, where multiple nodes might hold copies of the same data.
- **Cluster management**: A quorum decides which nodes form the active cluster, especially important for avoiding "split-brain" scenarios where a cluster might be divided into two parts, each believing it's the active cluster.
- **Consensus protocols**: In algorithms like Paxos or Raft, a quorum is crucial for achieving consensus among distributed nodes regarding the state of the system or the outcome of an operation.

**Advantages:**

- **Fault tolerance**: Allows the system to tolerate a certain number of failures while still operating correctly.
- **Consistency**: Helps maintain data consistency across distributed nodes.
- **Availability**: Increases the availability of the system by allowing operations to proceed as long as the quorum conditions are met.

**Challenges:**

- **Network partitions**: In cases of network failures, forming a quorum might be challenging, impacting system availability.
- **Performance overhead**: Achieving a quorum, especially in large clusters, can introduce latency in decision-making processes.
- **Complexity**: Implementing and managing quorum-based systems can be complex, particularly in dynamic environments with frequent node or network changes.

Quorum is fundamental in distributed systems and crucial for ensuring consistency, reliability, and availability when multiple nodes work together. It enhances fault tolerance, but introduces additional complexity and requires careful design and management to balance consistency, availability, and performance.

## Leader and follower

Distributed systems keep multiple copies of data for fault tolerance and higher availability. A system can use quorum to ensure data consistency between replicas (i.e., all read and writes are not considered successful until a majority of nodes participate in the operation). However, using quorum can lead to lower availability (at any time, the system needs to ensure that at least a majority of replicas are up and available, otherwise the operation fails). Quorum is also not sufficient, as in certain failure scenarios, the client can still see inconsistent data.

The solution is to allow only a single server (**leader**) to be responsible for data replication and to coordinate work. At any time, one server is elected as the leader. It becomes responsible for data replication and can act as the central point for all coordination. The followers only accept writes from the leader and serve as a backup. In case the leader fails, one of the followers can become the leader. In some cases, the follower can serve read requests for load balancing.

![Client, leader and followers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_13.png)

The leader entertains requests from the client and is responsible for replicating and coordinating with followers.

## Heartbeat

In a distributed environment, work/data is distributed among servers. To efficiently route requests in such setup, servers need to know what other servers are part of the system, and if they're alive and working. In a decentralized system, whenever a request arrives at a server, the server should have enough information to decide which server is responsible for entertaining that request. This makes the timely detection of server failure an important task, which also enables the system to take corrective actions and move the data/work to another healthy server and stop the environment from further deterioration.

The solution is that each server periodically sends a heartbeat message to a central monitoring server or other servers in the system to show that it's still alive and functioning.

Heartbeating is one of the mechanisms for detecting failures in a distributed system. If there's a central server, all servers periodically send a hearthbeat message to it. If there is no central server, all servers randomly choose a set of servers and send them a heartbead message every few seconds. This way, if no heartbeat message is received from a server for a while, the system can suspect that the server might have crashed. If there's no heartbeat within a configured timeout period, the system can conclude that the server is not alive anymore and stop sending requests to it and start working on its replacement.

## Checksum

In a distributed system, while moving data between components, it's possible that the data fetched form a node may arrive corrupted. This corruption can occur because of faults in a storage device, network, software, etc. How can a distributed system ensure data integrity, so that the client receives an error instead of corrupt data?

The solution is to calculate a checksum and store it with the data. To calculate a checksum, a cryptographic hash function is used (like MD5, SHA-1, SHA-256, or SHA-512). The hash function takes the input data and produces a string (checksum) of fixed length, containing letters and numbers. When a system is storing some data, it computes a checksum of the data and stores the checksum with the data. When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.


## Tradeoffs

## Discussing Trade-offs

Discussing trade-offs in a system design interview is important because:

- **Shows comprehensive understanding**: 
  - Balanced perspective: There're multiple ways to approach a problem, each with its advantages and disadvantages.
  - Depth of knowledge: There're different technologies, architectures, and methodologies, and choices impact a system's behavior and performance.
- **Highlights critical thinking and decision-making skills**:
  - Analytical approach: Analyze various aspects of a system, considering factors like scalability, performance, maintainability, and cost.
  - Informed decision-making: Make thoughful and informed decisions, ratherthan arbitrary.
- **Demonstrates real-world problem-solving skills**:
  - Practical solutions: Every system design decision comes with trade-offs. Perfect solutions rarely exist.
  - Prioritization: Prioritize certain aspects over others based on the requirements and constraints.
- **Reveals awareness of business and technical constraints**: 
  - Business acumen: Consider not just the technical but also the business implications of your design choices (cost implications, time to market…).
  - Adaptability: Adapt your design to meet different priorities and constraints (key in a dynamic business environment).
- **Facilitates better team collaboration and communication**:
  - Communication skills: Clearly articularting trade-offs is crucial for collaborating with team members and stakeholders.
  - Expectation management: Set realistic expectations and prepare for potential challenges in implementation.
- **Prepares for scalability and future growth**:
  - Long-term vision: Think about how the system will evolve over time and how early decisions might impact future changes or scalability.
- **Shows maturity and experience in handling complex projects**:
  - Professional maturity: Recognize that every decision has pros and cons.
  - Learning from experience: Apply lessons from past experiences to make better design choices.

## Strong vs Eventual Consistency







## Latency vs Throughput
## ACID vs BASE Properties in Databases
## Read-Through vs Write-Through Cache
## Batch Processing vs Stream Processing
## Load Balancer vs API Gateway
## API Gateway vs Direct Service Exposure
## Proxy vs Reverse Proxy
## API Gateway vs Reverse Proxy
## SQL vs NoSQL
## Primary-Replica vs Peer-to-Peer Replication
## Data Compression vs Data Deduplication
## Server-Side Caching vs Client-Side Caching
## REST vs RPC
## Polling vs. Long-Polling vs WebSockets vs. Webhooks
## CDN Usage vs Direct Server Serving
## Serverless Architecture vs Traditional Server-based
## Stateful vs Stateless Architecture
## Hybrid Cloud Storage vs All-Cloud Storage
## Token Bucket vs Leaky Bucket
## Read Heavy vs Write Heavy System



## Problems

## System Design Interviews guide
## System Design Master Template
## URL Shortening Service like TinyURL
## Pastebin
## Instagram
## Dropbox
## Facebook Messenger
## Twitter
## Youtube or Netflix
## Typeahead Suggestion
## API Rate Limiter
## Twitter Search
## Web Crawler
## Facebook’s Newsfeed
## Yelp or Nearby Friends
## Uber backend
## Ticketmaster



















## Synthesis

### Purpose of system design interviews

- Assessing problem-solving skills
- Evaluating technical knowledge
- Tradeoff analysis and decision-making
- Communication and collaboration

### Requirements

**Types:**

- **Functional:** What a system is supposed to do. Functions it must perform.
- **Non-functional:**: How the system performs a task. They're related to the quality attributes of the system (scalability, performance, availability, security…).

**Integrating both requirements**: Identify both requirements. Balance both and design a system that meets its functional goals while performing effectively, securely, and reliably. How to handle requirements: Ask questions, identify critical requirements, discuss tradeoffs, use real-world examples, and don't focus too much on one requirement type.

### Back-of-the-envelope estimations

**Back-of-the-envelope estimations:** Technique for quickly approximating values and making rough calculations using simple arithmetic and basic assumptions. They're not detailed or exact, but are useful for making informed decisions and tradeoffs. They help to:

- Indicate system scalability
- Validate proposed solutions
- Identify bottlenecks
- Demonstrate you thought process
- Communicate effectively design choices and their implications
- Quick decision making

**Techniques:**

- **Rules of thumb**: General guidelines/principles for making quick and reasonably accurate estimations. Based on experience and observations. Useful in the absence of detailed information.
- **Approximation**: Simplifying complex calculations by rounding numbers or using easier-to-compute values.
- **Breakdown and aggregation**: Break down a problem into smaller components, estimate each separately, and derive an overall estimate.
- **Sanity check**: Quick evaluation of an estimate to ensure its plausibility and reasonableness. This helps identify errors/oversights in the estimation process.

**Types:**

- __Load__: Requests/second, data volume, user traffic.
- __Storage__: Storage required for the generated data.
- __Bandwidth__: Network bandwidth needed to support traffic and data transfer.
- __Latency__: Response time and latency.
- __Resource__: Number of servers, CPUs, or memory required to handle the load and maintain desired performance.

**Process**:

- __Understand the scope__: Clarify the scale of the problem (how many users, how much data, …).
- __Use simple math__: Basic arithmetic.
- __Round numbers for simplicity__.
- __Be logical and reasonable__: Ensure your estimations make sense.

**Tips:**

- __Break down the problem__: Identify key components, estimate their requirements separately, and aggregate them.
- __Use reasonable assumptions__: Useful if you don't have all the necessary information.
- __Leverage your experience__: Use specific knowledge to inform your estimations. 
- __Be prepared to adjust your estimations__: The interviewer may provide additional information or challenge your assumptions.
- __Ask clarifying questions__: Ask questions if you're unsure about a requirement or assumption.
- __Communicate your thoughts__: Explain how you got your estimation and the assumptions you made.

### Things to avoid

- **Don't ignore the requirements:** Ask questions. Clarify requirements. Don't oversimplify or ignore complexities.
- **Don't dive into details too soon:** Establish high-level design first (architecture and components interactions).
- **Don't stick rigidly to one idea:** Consider alternatives. Don't ignore hints/feedback from the interviewer.
- **Don't overlook tradeoffs:** Discuss tradeoffs. Justify decisions.
- **Don't neglect non-functional requirements:** Don't focus solely on functional aspects. Consider real-world constraints.
- **Don't under-communicate:** Show your understanding and approach. Engage with interviewer, ask questions, listen to feedback.
- **Don't be overconfident/arrogant:** Don't dismiss feedback or overlook key aspects of the problem. Be open about what you're unsure.

### System design basics

When designing a large system, consider:

- What are the different architectural pieces that can be used?
- How do these pieces work with each other?
- How can we best utilize these pieces? What are the right tradeoffs?

Investing in scaling before it's needed is generally not a smart business proposition. However, some forethought into the design can save valuable time and resources in the future.

### Key characteristics of Distributed systems

Some of them are: Scalability, Reliability, Availability, Efficiency, Manageability.

- **Scalability:** Capacity to grow and manage increased demand (and work). Performance declines with the system size due to management or environment cost. Try to balance the load on all the participating nodes evenly. Scaling types:
  - **Horizontal**: Adding more servers into your resources pool.
  - **Vertical**: Scaling by adding more power to a server.

- **Reliability:** Ability to continue operating correctly and effectively in the presence of faults/errors/failures. Ability of the system to consistently meet the user's expectations over time. Adding redundancy can help, but has a cost.  Measures: _uptime_, _error rates_, _mean time between failures_ (MTBF).
  - __Fault tolerance__: Ability to continue operating (without total breakdown), maybe at a reduced level, even when some components fail, allowing to absorb/recover from faults. Measures: how quickly and effective the system detects, isolates and recovers from failures.

- **Availability:** Percentage of time a system remains operational to perform its required function in a specific period, under normal conditions.
  - __Reliability__: Availability over time considering the full range of possible real-world conditions that can occur. Reliability contributes to availability. But availability doesn't necessarily implies reliability.

- **Efficiency:** Ability of producing desired results with little resources. Measures: Latency (response time, delay), bandwidth (throughput, items delivered per second).

- **Manageability (or Serviceability):** Simplicity and speed with which a system can be repaired, maintained, or operated. Early detection of faults can decrease/avoid system downtime.

### Load balancing

**Load balancer (LB):** It spreads traffic across a cluster of servers (improving responsiveness and availability), and keeps track of the status of all resources while distributing requests. LB stops sending traffic to servers with issues (not available, not responding, or high error rate). LB typically sits between client and server (accepts incoming network and application traffic and distributes it across multiple backend servers).

For full scalability and redundancy, we can try to balance load at each system's layer:

- Between user and web server.
- Between web servers and internal platform layer (like application servers or cache servers).
- Between internal platform layer and database.

**Benefits of load balancing:**

- Users get faster, uninterrupted service.
- Service providers get less downtime and higher throughput.
- System administrators can easily handle incoming requests while decreasing wait time for users.
- System administrators experience fewer failed/stressed components.
- Some LBs provide predictive analytics that predict traffic bottlenecks.

**Health checks**: Servers health is monitored through health checks (regular attempts to connect to servers to ensure that they are listening). A server that fails a health check is automatically removed from the pool, and traffic will not be forwarded to it until it responds to health checks. 

**Redundant load balancers:** To prevent the LB from being a single point of failure, a second LB (passive) can be connected to the first (active) to form a cluster. Each LB monitors the health of the other and, if the main LB fails, the second LB takes over.

**Load balancing algorithms**: Used to select which server to send traffic to:

- __Least connection method__: To the server with fewest active connections. Useful for heterogeneous environments, variable traffic patterns, and stateful applications.
- __Least response time method__: To the server with lowest average response time. Useful for web services and APIs, and dynamic environments.
- __Least bandwidth method__: To the server currently serving the least amount of traffic measured in Mbps (megabits per second). Useful for content delivery networks, and real-time applications.
- __Round robin method__: Cycles through a list of servers and sends each new request to the next server. Useful for homogeneous environments (servers) and stateless applications.
- __Weighted round robin method__ (WRR): Each server has a weight (integer value indicating processing capacity). New connections are assigned to higher weight servers. The higher weight, the more connections it gets. Useful for heterogeneous server environments, scalable web application, and database clusters.
- __Weighted least connection__: Takes into account both the current load (active connections) and relative capacity (weight) of each server. Useful for heterogeneous server environments, high traffic web applications, and database clusters.
- __IP Hash__: A hash of the IP address of the client is calculated to redirect the request to a server. Useful for stateful applications, geographical distributed clients.
- __Random__: Distributes incoming requests to servers randomly. Useful for homogeneous environments, stateless applications, and simple deployments.
- __Custom load__: You define the metrics and rules for distributing incoming traffic across a pool of servers. Useful for complex applications, highly dynamic environments, custom requirements.

### Caching

**Locality of reference principle:** Recently requested data is likely to be requested again. Caches take advantage of this principle.

**Cache:** High-speed storage layer that sits between the applications and the original source of the data (database, file system, remote web service…). When the application requests data, it's first checked in the cache. If the data is found in the cache, it's returned to the application; otherwise, it's retrieved from its original source, stored in the cache for future use, and returned to the application. It's used in almost every computing layer (hardware, OSs, web browsers, web applications…), with various types of data (web pages, database queries, API responses, images, videos…). Caching's goal is to reduce the number of times data needs to be fetched from its original source, resulting in faster processing and reduced latency.

Load balancing helps you scale horizontally across an ever-increasing number of servers. Caching enables you to make vastly better use of the resources you already have and makes otherwise unattainable product requirements feasible.

**Concepts:**

- __Cache__: Temporary storage location for data or computation results, typically designed for fast access and retrieval.
- __Cache hit__: When a requested data item or computation result is found in the cache.
- __Cache miss__: When a requested data item or computation result is not found in the cache and needs to be fetched form the original data source or recalculated.
- __Cache eviction__: Process of removing data from the cache, typically to make room for new data or based on a predefined cache eviction policy.
- __Cache staleness__: When data in the cache is outdated compared to the original data source.

**Types of caching:** Caching can be implemented in various ways, depending on the use case and type of data. Some common types are:

- **In-memory caching:** Stores data in the main memory of the computer, which is faster to access than disk storage. Useful for frequently accessed data that fits into memory. Commonly used for caching API responses, session data, and web page fragments. Some implementation techniques are including custom caching logic within the application code, and using a cache library (Memcached, Redis…).

- **Disk caching:** Stores data on the hard disk, which is slower than main memory but faster than retireving data from a remote source. Useful for data too large to fit in memory or for data that needs to persist between application restarts. Commonly used for caching database queries and file system data.

- **Database caching:** Stores data in the database itself, reducing the need to access external storage. Useful for data stored in a database and frequently accessed by multiple users. Some implementation techniques are database query caching and result set caching.

- **Client-side caching:** Stores frequently accessed data (images, CSS, JavaScript files…) to reduce the need of repeated requests to the server. It occurs on the client device (web browser, mobile app…). Examples: browser caching, local storage, etc.

- **Server-side caching:**: Used to store frequently accessed data, precomputed results, or intermediate processing results to improve the performance of the server. It occurs on the server (typically, web applications or other backend systems). Examples: full page caching, fragment caching, object caching, etc.

- **CDN caching:** Stores data on a distributed network of servers, reducing the latency of accessing data from remote locations. useful for data accessed from multiple locations around the world (like images, videos, and other static assets). Commonly used for content delivery networks and large-scale web applications.

- **DNS caching:** Cache used in the DNS (Domain Name System) to store results of DNS queries for a period of time. The computer (user) trying to access a website sends a DNS query to a DNS server to resolve the website's domain name to an IP address. The DNS server responds with the IP address, which the computer uses to access the website. When a DNS server receives a request for a domain name, it checks its local cache to see if it has the corresponding IP address. This reduces response time for DNS queries (no need to query other servers) and improves the overall performance of the system (reduced number of queries).

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_5.png)

**Cache invalidation:** We must ensure that the data in the cache is still correct. Otherwise, we serve out-of-date (stale) information.

- __Ensure data freshness__: When the underlying data changes (prices, names…), mark or remove the old cached data (cache invalidation). Otherwise, caches will serve outdated data and lead to inconsistencies across your application.
- __Maintain system consistency__: Large systems often have multiple caching laryers. If any layer serves old data while others serve new data, user can get conflicting information. Properly invalidating caches at each layer helps maintain a consistent view of your system's state.
- __Balance performance and accuracy__: Cache invalidation strategies (time-to-live/TTL, manual triggers, even-based invalidation…) are designed to minimize the performance cost of continuously refreshing the cache. The goal is to keep data as accurate as possible while still still getting high-speed data retrieval.
- __Reduce errors and mismatched states__: When caches go stale, you risk presenting users wrong or invalid information. Strategically invalidating caches when data changes reduces these odds.

**Cache invalidation schemes**: There are 3 main schemes that are used:

- __Write-through cache__: Data is simultaneouly written into the cache and the corresponding database (permanent storage). This allows for fast retrieval, keeps consistency between cache and storage, and ensures no data is lost during a system disruption (crash, power failure…). However, since every write operation is done twice before returning success to the client, it causes higher latency for write operations.
- __Write-around cache__: Similar to write-through cache, but data is written directly to permanent storage, bypassing the cache. This reduce the cache being flooded with write operations that will not subsequently be re-read. However, a read request for recently written data will create a "cache miss" and must be read from slower back-end storage, causing higher latency.
- __Write-back cache__: Data is written to cache alone. Writting to permanent storage is done after specified intervals or under certain conditions. This results in low-latency and high-throughput for write-intensive applications. However, since the only copy of the written data is in the cache, there's risk of data loss during a system disruption.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_6.png)

**Cache invalidation methods:** Most famous ones are:

- **Purge:** Remove cached content for a specific object, URL, or set of URLs. When a purge request is received, the cached content is immediately removed. Typically used when there's an update or change to the content and the cached version is no longer valid.
- **Refresh:** Update cached content with the latest version. When a refresh request is received, the cached content is updated with the latest version from the origin server.
- **Ban:** Invalidate cached content based on specific criteria (URL pattern, header…). When a ban request is received, any cached content matching the specified criteria is immediately removed.
- **TTL (Time-to-live) expiration:** Set a time-to-live value ofr cached content, after which the content is considered stale and must be refreshed. When a request for a content is received, the cache checks the TTL value and serves the cached content if it hasn't expired. Otherwise, it fetches the latest version from the origin server and caches it.
- **Stale-while-revalidate (SWI):** Serve stale content from cache while content is updated in the background. When a request for content is received, the cached version is immediately served, and an asynchronous request is made to the origin server to fetch the latest version of the content to update the cached version. This ensures content is served quickly, even if it's slightly outdated. Used in browsers and CDNs.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_7.png)

**Cache read strategies:** Two famous ones are:

- **Read through cache:** The cache is responsible for retrieving the data from the underlying data store when a cache miss occurs. After a cache miss, cache retrieves data from the data store, updates cache, and returns data to the application. The application requests data from the cache instead of the data store directly. It maintains consistency between cache and data store, and simplifies code. Useful when data retrieval from data store is expensive, and cache misses are relatively infrequent.

- **Read aside cache (or cache-aside, or lazy loading):** The application is responsible for retrieving data from the underlying data store when a cache miss occurs. The application first checks the cache for the requested data. If not found (cache miss), the application retrieves it from data store, updates cache, and uses the data. This provides better control over the caching process, but adds complexity to the application code. Useful when you need to ensure that a cache failure won't take down your whole system, or when you want to optimize cache usage based on specific data access patterns.

![Cache types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_8.png)

**Cache eviction policies:** Most common ones are:

- **FIFO (First In First Out)**: The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.
- **LIFO (Last In First Out)**: Similar to FIFO, but it evicts the block accessed most recently first.
- **LRU (Least Recently Used)**: Discard the least recently used items first.
- **MRU (Most Recently Used)**: Discards the most recently used items first.
- **LFU (Least Frequently Used)**: Discards the least often used items first.
- **RR (Random Replacement)**: Randomly selects an item and discards it to make space when necessary.

## Data partitioning

**Data partitioning:** Process of dividing a large database (DB) into smaller, more manageable parts called **partitions** or **shards**. Each partition is independent and contains a subset of the overall data. Each partition is assigned to a separate processing node, which performs operations on its data subset independently of others. Datasets are partitioned based on a certain criterion. Advantages:

- Data partitioning can improve performance and scalabitily of large-scale data processing applications, as it allows processing to be distributed across multiple nodes, minimizing data transfrer and reducing processing time.
- Distributing data across multiple nodes/servers, the workload can be balanced, and the system can handle more requests and process data more efficiently.

Most popular **partitioning schemes** for large-scale applications are:

- **Horizontal partitioning** (Sharding): Divides a database into multiple partitions (shards), with each one containing a subset of rows. Each shard is typically assigned to a different database server, allowing for parallel processing and faster query execution times. However, this can lead to unbalanced servers if the value whose range is used for partitioning isn't chosen carefully.
  - Example: Social media platform that stores user data in a database table. The user table might be partitioned horizontally based on the geographic location of users, so that users in different countries are stored in different shards. This way, when a user logs in and his data needs to be accessed, the query can be directed to the appropriate shard, minimizing the amount of data that needs to be scanned.

- **Vertical partitioning**: Splits a database table into multiple partitions (shards), with each one containing a subset of columns. This can optimize performance by reducing the amount of data to scan, especially when certain columns are accessed more frequently than others.
  - Example: E-commerce website that stores customer data in a database table. The customer table might be partitioned vertically based on the type of data (personal information in one shard, order history and payment information in another). This way, when a customer logs in and their order history needs to be accessed, the query is directed to the appropriate shard, minimizing the data to scan.

- **Hybrid partitioning**: Combines horizontal and vertical partitioning. It helps optimize performance by distributing data evenly across multiple servers, while minimizing the data to scan.
  - Example: Large e-commerce website that stores customer data in a database table. The customer table might be partitioned horizontally based on customer's geographic location, and then each shard partitioned vertically based on data type. This way, when a customer logs in and his data needs to be accessed, the query can be directed to the appropriate shard, minimizing the data to scan; and each shard can be stored on a different database server, allowing for parallel processing and faster query execution times.

![Partition schemes](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_9.png)

**Partitioning criteria**: Factors or characteristics of data that can be used to divide a large dataset into smaller partitions. Most common criteria are:

- **Key or Hash-based partitioning**: Apply a hash function to some key attributes of the entity we are storing (this yields the partition number).
  - Example: We have 100 DB servers and our ID is a number that gets incremented by one each time a new record is inserted. Here, the hash function could be `ID % 100`, which gives us the server number where we can store/read that record. This ensures uniform allocation of data among servers. However, this fixes the total number of DB servers, so adding new servers requires changing the hash function, redistributing data, and downtime for the service. A workaround for this problem is using [**consistent hashing**](#consistent-hashing).

- **List partitioning**: Each partition is assigned a list of values. Whenever we want to insert a new record, we see which partition contains our key and then store it there.
  - Example: All users living in Iceland, Norway, Sweden, Finland, or Denmark are stored in a partition fo the Nordic countries.

- **Round-robin partitioning**: With n partitions, the i tuple is assigned to partition i % n. Simple strategy that ensures uniform data distribution.

- **Composite partitioning**: Combine any of the above partitioning schemes to devise a new scheme.
  - Example: First apply a list partitioning scheme and then a hash-based one. Consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key-space to a size that can be listed.

**Common problems of data partitioning**: Operations across multiple tables/rows in the same table doesn't run on the same server. This causes extra constraints on the operations that can be performed.

- **Joins and Denormalization**: Performing joins on a database running on one server is straightforward. However, it's often not feasible to perform joins that span database partitions (cross-partition queries on a partitioned database are not feasible). They're not efficient (data has to be compiled from multiple servers). Common workaround: denormalize the database so that queries that previously required joins can be performed from a single table, though this requires to deal with denormalization's perils (like data inconsistency).

- **Referencial integrity**: Enforcing data integrity constraints (like foreign keys) in a partitioned database can be extremely difficult. Most RDBMS don't support foreign keys constraints across databases on different servers, so applications requiring referencial integrity on partitioned databases often have to enforce it in application code (this often requires applications to regularly run SQL jobs to clea up dangling references.

- **Rebalancing**: There're many reasons for changing our partition scheme:
  1. Data distribution is not uniform (example: there're a many places for a ZIP code that cannot fit into one database partition).
  2. There's a lot of load on a partition (example: too may requests are handled by the DB partition dedicated to user photos.
  - In such cases, either we have to create more DB partitions or have to rebalance existing partitions, which means the partitioning scheme changed and all existing data moved to new locations. It's extremely difficult to do this without incurring downtime. Using a scheme like directory-based partitioning does make rebalancing more palatable, but increases the complexity of the system and creates a new single point of failure (the lookup service/database).


## Indexes

Sooner or later there comes a time when a database performance is no longer satisfactory. That's when you should apply **database indexing**. Creating an index on a particular table in a database can make it faster to search through the table and find the row/s that we want. Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

Example: A library catalog is a register that contains the list of books found in library. It's organized like a database table generally with four columns: book title, writer, subject, and date of publication. There're usually 2 such catalogs: one sorted by book title and one sorted by writer name. This way, you can either look by writer or by title. These catalog are like indexes for the database of books. They provide a sorted list of data that is easily searchable by relevant information.

An index is a data structure that can be perceived as a table of contents that points us to the location where actual data lives. When we create an index on a column of a table, we store that column and a pointer to the whole row in the index.

![Database index](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_10.png)

To use indexes we must consider how users will access the data. In the case of data sets of big size (many terabytes) and small payloads (e.g., 1 KB), indexes are a necessity for optimizing data access. Finding a small payload there requires iterating over too much data in an unreasonable time. Furthermore, if that data set is spread over several physical devices, we need a way to find the correct physical location of the desired data. Indexes are the best way to do this.

An index can dramatically speed up data retrieval, but a too large index can slow down data insertion, update, and deletion. Adding rows or making updates to existing rows for a table with an active index requires writing the data and updating the index, which decreases performance. Thus, avoid adding unnecessary indexes on tables, and remove those that are no longer used. Addind indexes improve search queries. If the goal of the database is to provide a data store that is often written to and rarely read from, decreasing the performance of the more common operation (writing) is probably not worth the increase in performance of reading.

More information: [Database index](https://en.wikipedia.org/wiki/Database_index)


## Proxies

**Proxy server**: Intermediate piece of software or hardware that sits between the client and the server to facilitate traffic. Typical use cases:
- Traffic control: Routes requests to the appropriate servers. Coordinates requests from multiple servers. Clients connect to a proxy to make a request for a service like a web page, file, or connection from the server.
- Optimize request traffic: It can optimize request traffic from a sytem-wide perspective by combining the same data access requests into one request and then return the result to the user (**collapsed forwarding**). If several nodes request the same data, and it is not in cache, the proxy can consolidate these requests into one so that we will only read data from disk once.
- Logging: Log requests.
- Filter requests.
- Request transformation: By adding/removing headers, encrypting/decrypting, or compressing a resource.
- URL/Content rewriting: 
- Caching: Cache data.
- Load balancing: Distributes incoming traffic across multiple backends.

**Forward proxy**: It can hide client's identity (useful for protecting clients on your internal network). It facilitates the request for resources from other servers on behalf of clients, thus anonymizing the client from the server. Focused on outbound traffic (it governs what a group of internal users can do on the open internet).

**Reverse proxy**: It can hide server's identity (useful for protecting your servers). It retrieves resources from one or more servers on behalf of a client. These resources are returned to the client, appearing as if they originated from the proxy server itself, thus anonymizing the server. Focused on inbound traffic (it governs hwo the open internet accesses a group of internal servers). Other use cases: DDoS protection, Canary experimentation (like routing 5% of users to a new version of a site).
- Example: A client making a request to `facebook.com` gets served by a reverse proxy server, which gets the response from one of the backend servers and returns it to the client.

![Proxy servers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_11.png)


## Redundancy and Replication

[**Redundancy**](https://en.wikipedia.org/wiki/Redundancy_(engineering)): Duplication of critical components or functions of a system with the intention of increasing the reliability of the system (usually in the form of a backup or fail-safe), or to improve actual system performance. This removes the single points of failure in the system and provides backups if needed in a crisis.

- Example 1: Just having a file in a single server means that if we lose the server, we lose the file. Having a duplicate or redundant copies of the file solves this problem.
- Example 2: If we have 2 instances of a service running in production and one fails, the system can failover to the other one.

Database **replication**: Process of copying and synchronizing data from one database to one or more additional databases. This is commonly used in distributed systems where multiple copies of the same data are required to ensure data availability, fault tolerance, and scalability. It's widely used in many database management systems (DBMS), usually with a primary-replica relationship between the original and the copies. The primary server gets all the updates, which then ripple through to the replica servers. Each replica outputs a message stating that it has received the update successfully, thus allowing the sending of subsequent updates. Most typical database replication strategies:

- **Synchronous replication**: Changes made to the primary database are immediately replicated to the replica databases before the write operation is considered complete. The primary database waits for the replica databases to confirm that they have received and processed the changes before the write operation is acknowledged. This ensures data consistency across all databases and reduces the risk of data loss or inconsistency.

- **Asynchronous replication**: Changes made to the primary database are not immediately replicated to the replica databases, but are queued and replicated to the replicas at a later time. There's a delay between the write operation on the primary database and the update on the replica databases, which can result in temporary inconsistencies between databases. This makes write operations faster, and allows write operations to be completed if one or more replica DBs are unavailable (the system remains available).

- **Semi-synchronous replication**: Combination of synchronous and asynchronous replication. Changes made to the primary database are immediately replicated to at least one replica database, while other replicas may be updated asynchronously. The write operation on the primary DB is not considered complete until at least one replica DB has confirmed that is has received and processed the changes. This ensures some level of storng consistency between the primary and replica DBs, and provides improved performance compared to fully synchronous replication.

![Replication types](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_12.png)


## SQL vs. NoSQL

**SQL** and **NoSQL** are two different approaches to storing and managing data, each one with its own organization method and strengths.

### SQL databases (Relational databases)

**Relational databases** are the traditional ones. They shine when you need strong consistency, structured data with defined relationships, and the ability to perform complex queries. However, they can be less flexible with changes and face challenges in scaling out horizontally. Characteristics:

- **Relational data model**: Data is organized into tables (**relations**) with rows and columns. Each table represents an **entity**, and relationships between tables are defined via **foreign-keys**. Data is **structured and schema-based**, meaning your must define the schema (table structure) in advance. Example: `Users` table and `Orders` table have a relationship (via `userID`) linking orders to the user who placed them.

- **ACID properties** (Atomicity, Consistency, Isolation, Durability): Transactions in SQL databases are reliable; either all steps of a transaction complete or none do (atomicity), and the DB remains consistent and isolated during operations, with changes durable upon completion. Useful for banking applications (transferring money should not half-complete, but must deduct from one account and add to another in one atomic action).

- **SQL** (Structured Query Language): Relational databases are manipulated using SQL, a declarative query language. You specify **what** data you want (declaration), and the DB engine figures **how** to get it. This makes SQL DBs excellent for **complex queries and analytics** because you can leverage joins, aggregations (`GROUP BY`), sorting, and filtering directly in the database. Example: You can write a query to join multiple tables and filter results in one command, and the DB's query planner and optimizer will determine the best way to execute it.

- **Examples**: MySQL, PostgreSQL, Oracle, Microsoft SQL Server.

- **Use cases**: SQL DBs are best suited for applications where data is higly structured and relationships matter. Examples: financial systems and banking (transactions and consistency are critical), e-commerce platforms (orders, customers, inventory with complex relationships), and any scenario requiring multi-row transactions or sophisticated querying across data.

### NoSQL databases (Non-relational databases)

**Non-relational databases**: Broad category. More flexible and scalable. They suit modern, large-scale applications. They shine when you need to handle big data, fast. Characteristics:

- **Flexible data models**: Doesn't require a predifined schema. They can store unstructured or semi-structured data easily, and each record (or document) can have its own unique structure. Thus, you can add new fields on the fly without a painful migration. There're different types, each optimized for a certain data model.

  - **Document databases**: Data is stored in documents (JSON, BSON, …). Each document is a self-contained record (like a JSON object), which can have nested fields. Useful for data that naturally fits a hierarchical structure (like a blog post with comments, tags, …). Examples: MongoDB, CouchDB.
  - **Key-value stores**: Simplest NoSQL form. Data is stored as a key and an associated value (string, JSON, BLOB, …). It's like a big hash table or dictionary. Very fast for simple lookups by key. Example: Redis, Amazon DynamoDB.
  - **Wide-columns stores**: This use tables, but each row can have a different set of columns. They're optimized for large-scale, distributed data storage across many commodity servers. Examples: Apache Cassandra, HBase.
  - **Graph databases**: Designed for data where relationships are central. Data is stored as nodes and edges (edges represent relationships between nodes). Excellent for traversing complex relationship graphs. Examples: Neo4j, Amazon Nepture.
  - **Other NoSQL types**: In-memory databases, time-series databases, ledger databases, etc.

- **Schema flexibility**: Due to their schema-less nature, NoSQL DBs allow you to evolve your data model easily. If you need to store new attributes, you can just start storing them (no `ALTER TABLE` meeded). This is ideal for agile development environments or use cases where the data model isn't fully known upfront or changes frequently.

- **Horizontal scalability**: They're designed to scale out horizontally across multiple servers (cluster of machines) rather than just scaling up a single server. Thus, you can handle huge volumens of data and traffic by distributing the load. Many NoSQL DBs achieve scaling through sharding (partitioning data across nodes) and replication. Example: Cassandra and DynamoDB automatically distribute data based on keys, allowing them to handle web-scale workloads across many servers.

- **BASE and Eventual consistency**: Most NoSQL databases relax some of the ACID guarantees to achieve high scalability and availability. They often follow the BASE philosophy: Basically available, Soft state, Eventual consistency. This means they might allow temporary inconsistencies (different nodes might not have the exact same data at every moment), but they aim to converge to consistency over time (eventual consistency) (see [CAP theorem](#cap-theorem)). Not all NoSQL DBs are eventually consistent, but often strict consistency is traded for performance/availability. Some NoSQL systems (like MongoDB) can be configured for strong consistency in certain operations, but the general pattern is looser consistency.

- **High performance for specific use cases**: NoSQL DBs are often optimized for high performance on specific workloads. Thus, they are great for powering real-time analytics, fast web aplications, and other scenarios where speed is more critical than perfect consistency at every moment. Examples:

  - Key-value stores (like Redis) can handle millions of reads/writes per second for simple get/set operations (often used for caching). Wide-columns stores (like Cassandra) excel at write-heavy loads (logging, time-series data). Because they avoid the overhead of joins and often store data in a denormalized way, they can retrieve related data in a single read.

- **Examples**: MongoDB (document store), Apache Cassandra (wide-column store), Amazon DynamoDB (key-value store), Redis (in-memory key-value store), CouchDB (document store), Neo4j (graph database).

- **Use cases**: NoSQL is used when we have large volumes of rapidly changing or unstructured data, or requirements for massive scale and distributed access. Examples: social media platforms (storing posts, likes, messages, acros distributed clusters), content management and user-generated content systems, IoT and real-time analytics (inserting tons of events per second), gaming and ad tech (high throughput reads/writes), and caching layers.

### Key differences

- **Schema**:

  - **SQL** DBs require a predefined schema: Tables and columns (with data types) must be designed upfront, and this schema dictates what data can go into the table. The data is relational: you often normalize data into multiple tables to avoid duplication, then use relationships (joins) to query across them. This approach enforces data integrity (e.g., you can ensure via constraints that every order has a valid user), but it's rigid (changing a schema can be a big operation involving migrations and potential downtime).

  - **NoSQL** DBs are schema-flexible (or schema-less) by design. Each record (document, key-value pair, etc.) can have its own shape (e.g., one document in a MongoDB collection can have fields that another document in the same collection doesn't). This is ideal for unstructured or semi-structured data where you might not know all fields in advance. Developers can iterate quickly, adding new fields as needed without touching a central schema definition. However, without a strict schema, ensuring data consistency and integry is pushed to the application level (be careful with what you insert, because the DB won't enforce a many rules). In practice, teams often impose implicit schemas or use ORMs (Object-Relational Mapping) that validate data, but the DB itself is forgiving about structure.

- **Data model** (data relationships):

  - **SQL** relationships (one-to-one, one-to-many, many-to-many) are first-class and enforced through foreign keys and join operations. Example: you might have separate tables for `Users` and `Posts` and join them to get a user's posts. Useful if data is highly structured and you benefit from a strict schema with clear relationships.

  - **NoSQL** relationships are usually handled differently. Many NoSQL use cases favor denormalizing data, that is, storing related data together to avoid needing joins (because cross-document joins are not natively supported or efficient in most NoSQL systems). Example: in a document store, you might store user info and their posts in a single document or use a reference and handle the join logic at the application level. Document DBs can store related info together (nested), which can simplify data retrieval at the cost of duplication. Useful if data is variable or you expect the schema to evolve, or you're dealing with hierarchical data that fits better in JSON.

- **Scalability** (Vertical vs. Horizontal): 

  - **SQL** DBs are traditionally scaled vertically (scale up), meaning that if you need to handle more load, you use a bigger machine (more CPU, more RAM, faster disk/SSDs, etc.). This has a physical and cost limit (high-end hardware is expensive and finite). SQL DBs can be scaled horizontally using techniques like sharding (partitioning the data across multiple servers) or using read replicas for distributing read traffic. However, horizontal scaling in SQL is hard and not straightforward (maintaining consistency across shards, performing joins across shards, or handling multi-shard transactions adds complexity), so companies often use a single big SQL server or a primary-replica setup, until sharding is absolutely necessary. Newer technologies and distributed SQL/NewSQL DBs (like Google Spanner, CockroachDB) are tackling these challenges. Typical SQL approach: Scale up first, then carefully scale out if you must.

  - Most **NoSQL** DBs are built with the idea of an easy horizontal scaling (scale out) by adding more commodity servers. They're designed to distribute data across nodes and handle partitioning natively (e.g., adding 5 nodes to a cluster of 10 nodes might automatically rebalance data to use the new nodes). Useful for very large datasets or applications expected to grow rapidly. Massive throughput and storage can ve achieved by clustering. Many cloud services (AWS DynamoDB, Azure Cosmos DB…) are NoSQL stores that can auto-scale behind the scenes (you just pay for more throughput or nodes). To enable scaling, some sacrifice is done (like strong consistency or join capability). Example: Cassandra can handle billions of writes per day across a distributed cluster, something a single SQL instance would struggle with. SQL is useful if your data size and traffic are moderate to high but can be handled by beefing up a single server (or a primary-replica setup), though you should plan carefully if you ever hit the ceiling and need sharding

  - **Why horizontal scaling is hard for SQL?** SQL doesn't shard as easily. Its strong consistency and relational constraints need all nodes to be in sync on transactions. Queries that need data from different shards are complex. Jois across shards either are not possible or require distributed queries that are slow. Also, ACID transactions across multiple nodes require two-phase commit or other protocols which are complex and can slow things down. SQL's design assumes a single node or a tightly coupled cluster. In contrast, NoSQL systems often don't allow multi-document transactions (or limit them) and accept eventual consistency, making it easier to partition data without strict ordering between partitions. NoSQL's shared-nothing architecture aligns with horizontal scaling. NoSQL is useful if you anticipate the need to scale massively by adding lots of servers.

  - **NewSQL**: Type of modern DBs that try to blend both: offer SQL interface and ACID transactions, but with a distributed, horizontally scalable backend (e.g., Google Spanner, CockroachDB). They often use TrueTime and consensus algorithms to maintain consistency at scale.

- **Consistency, Transactions, and the CAP theorem** (ACID vs. BASE):

  - **SQL** prioritize strong consistency. Under ACID properties, when a transaction is committed to a SQL DB, all user querying the data (assuming they're not in the middle of their own transaction isolation) will see the same, up-to-date data. This is useful for bank accounts or inventory (two people shouldn't see the same $100 as available to withdraw, or sell the last item to two buyers). SQL DBs are often categorized as CP (Consistent & Partition-tolerant) in the CAP theorem (they choose consistency over availability when partitioned. So, if a SQL DB node can't reach others, it might refuse to serve some data rather than serve possibly inconsistent info. SQL's robust handling of transactions mean you can bundle multiple operations (debit one account, credit another…) into one unit that either fully succeeds of fully fails, maintaining data integrity.

  - Many **NoSQL** DBs, especially those designed to distribute across many nodes, favor availability and partition tolerance over strong consistency. They allow eventual consistency (data updates propagate to nodes over time, and for a brief period, different clients might read different data from different replicas). They tend to follow the BASE approach (Basically Available, Soft state, Eventual consistency). This is acceptable in many scenarios (like social feeds, where a slight delay is fine), but unnaceptable in others (like a financial transaction ledger).

    - Example: If you update a user's profile picture in a globally distributed NoSQL store, it might update in the US data center immediately but take a second to update in the Europe replica. A reading in Europe in that second might get the old picture (stale data), but after a short time, consistency is achieved (eventually consistent).

  - **Transactions in NoSQL**: Traditionally, NoSQL systems either didn't support multi-document transactions or had limited transaction support. The idea was to keep things simple and fast by operating mostly on single records (which are often designed to contain all related info needed for a given operation, avoiding the need for multi-object transactions). However, many modern NoSQL DBs have added some level of transactions. Example: MongoDB added multi-document transaction support (with ACID properties) in version 4.x for scenarios that need it. Still, using transactions in NoSQL is the exception rather than the norm, and often with performance or complexity trade-offs. If your application requires a lot of complex transactions spanning multiple pieces of data, SQL has a clear edge.

  - **CAP theorem**: A distributed system can only guarantee two our of three: Consistency, Availability, Partition tolerance. SQL DBs often choose Consistency + Partition tolerance over availability (especially clustered relational DBs). They'd rather be consisten and maybe not respond (or fail) if partitions happen. NoSQL (certain types, like Dynamo-style or Cassandra) often choose Availbility + Partition tolerance over consistency, thus providing high uptime and partition resilience at the cost of sometimes returning stale data. This is not universal (though there're strongly consistent NoSQL systems and highly available SQL setups), but is a general rule.

  - **ACID vs BASE**:
    - ACID (SQL) is about absolute correctness and consistency, critical for ordered, reliable transactions (like financial or legal data). An SQL DB is safe for applications that cannot tolerate inconsistent or out-of-data data and transactions.
	- BASE (NoSQL) is about being basically available and allowing inconsistency as a trade for performance and partition tolerance, often acceptable for large-scale web systems (like showing slightly out-of-data info that soon syncs). A NoSQL DB works better if you can tolerate eventual consistency and need to prioritize uptime and distribution (like a globally distributed app that should always accept writes even if nodes are partitioned).

- **Query capabilities and performance**:

  - **SQL** has rich query capabilities (join multiple tables, filter, sort, group by, use subqueries, window functions, and perform complex analytics all within the DB query). The DB engine (optimized for decades) execute them efficiently using indexes, execution plans, etc. Useful for ad-hoc queries or heavy analytical reporting on transactional data. Complex queries can have not good performance, but a well tuned SQL DB cna ahndle quite a lot on a single machine, espeically with proper indexing.

  - **NoSQL** DBs generally don't support joins (with few exeptions or limited forms). The query languages vary: some use SQL-like query languages (e.g., Cassandra has CQL, which looks like SQL for a single table; MongoDB has a JSON-based query syntax, …), but they're typically limited to fetching data by keys or simple filters within a single collection/table. For any relationship-based query, you often have to denormalize (i.e., sotre data together) so that your query doesn't need to fetch from multiple places. Many NoSQL users design their data model starting from the query patterns (_How will I need to access this data?_) and then collocate data accordingly. This makes NoSQL blazing fast for specific queries it's design for (since all needed data might be in one document or one key lookup), but makes ad-hoc queries or new query patterns harder (e.g., if you suddenly want to find "all users who posted more than 100 comments last year", and your data wasn't designed for that, you might have to scan lots of documents or even use external processing).
  
  - **Analytics and OLAP** (Online Analytical Processing):
    - For heavy analytics (OLAP), traditionally you'd use an SQL data warehouse or at least be able to export data from your SQL DB to analytical DBs. SQL DBs integrate very well with reporting tools, BI platforms, etc., due to the ubiquity of SQL.
	- NoSQL is catching up in analytics (e.g., tools like Hive allow SQL-like querying on top of NoSQL stores, and some NoSQL have aggregation frameworks), but the maturity and tooling for analytics on SQL are far richer.

  - **Full-text search of Geospacial**: These are specialized query types. Many SQL DBs have some support (like full-text indexes in MySQL or PostGIS for geospatial in PostgreSQL). NoSQL might integrate with other tools (e.g., use Elasticsearch for text search alongside a NoSQL store). If your use case needs special queries, consider if your DB choice support them or if you need a companion system. Performance considerations:
    - For **simple queries** (like key lookups or fetching a document by ID), NoSQL can be extremely fast, especially if the data is partitioned and replicated to be local to the user's region, etc. A key-value store can often outperform a relational database for simple get/put operations because it cuts out the overhead of SQL layer and joins.
	- For **complex queries**, a single SQL query might outshine multiple NoSQL calls. For instance, to get data that's spread across tables in SQL, you do one join query. In NoSQL, you might have to do several separate lookups from different collections or do a lot of client-side filtering. This can introduce more network calls and client-side processing, which reduces performance.
	- **Indexing**: Both SQL and NoSQL DBs use indexes to speed up lookups. In SQL, you index columns; in NoSQL, you might index fields in documents (e.g., MongoDB has indexes too). Performance in both depends on good indexing for query patterns. NoSQL often encourages using the primary key (or partition key) as the main query mechanism (like how DynamDB expects you to query by primary key; anything less is a full scan unless you add secondary indexes which are limited).
	- **Write performance**: Many NoSQL systems are optimized for fast writes (e.g., Cassandra has high write throughput thanks to its log-structured storage engine and distributed nature). SQL DBs can often handle fast writes as well, but their focus on immediate consistency can introduce overhead (locking, transaction coordination). For write-heavy workload (like logging millions of events), a NoSQL store might accept writes more readily (Cassandra, DynamoDB, etc., are often used for logging and telemetry for this reason).
	- **Read performance**: It depends on the query type. For simple key-value reads, NoSQL is great. For complex reads that aggregate data, SQL shines. Caching strategies often come into play too (e.g., using Redis to cache results on SQL queries, or using a search index for complex text queries).
	- **Bottom line**: For complex querying and reporting, SQL DBs offer more power out-of-the-box. For fast reads/writes on simple access patterns at huge scale, NoSQL DBs often provide better performance (since they can distribute the load and don't have the overhead of multi-table operations). Try to match your expected query patterns to the DB's strengths.

- **Flexibility and Development speed**:

  - In **SQL**, since you have a strict schema, you typically do data modeling upfront. Think about your entities, design normalized tables, and set up constraints. This can enforce good discipline and yield an efficient design for data integrity. However, if requirements change and you need to add a new field or change structures, it often involves an `ALTER TABLE` and possibly updating existing records to have default value, etc. In a large production environment, schema changes must be done carefully to avoid downtime. This rigidity means iterating quickly can be harder. In early development or prototyping, the schema may slow you down if you need to keep changin it. However, many ORMs and migration tools exist to manage this, and some developers prefer the clarity of an enforced schema.

  - In **NoSQL**, its schemaless nature lets you develop features faster initially. If you need a new piece of data stored, just start storing it. If one record has extra fields, that's fine. This can speed up development since you don't have to perform migrations for every little change, and aligns well with agile methodologies where requirements evolve. However, if you're not careful, you might end up with messy or inconsistent data structures over time (technical debt in data modeling). Also, while NoSQL allows flexible writes, when reading you still often need to handle multiple shapes of data (e.g., some documents have field X, some don`t) (called schema-on-read: you impose structure when reading out the data, instead of on write).
  - **Ecosystem and tooling**: The SQL ecosystem is very mature. There're tons of tools for reporting, TEL (extract-transform-load), backup, monitoring, ORMs, etc. Most developers learn SQL at some point. Many frameworks seamlessly integrate with SQL DBs. NoSQL, being diverse, has varied ecoystems. Some systesm like MongoDB have a strong community and many libraries, but not many off-the-shelf tools for complex operations (like a join across collections) because that's not what it's built for. NoSQL has a learning curve, both for query patterns and understanding the specific DBs behavior (consistency quirks, etc.).
  - **Maintenance and operations**: Complexity depends on the architecture. SQL has well-established best practices, while NoSQL rapid evolution require staying updated on improvements and patterns.
    - Running a single SQL DB can be simpler than managing a cluster of many nodes.
	- NoSQL's distributed nature means ops teams must handle node failures, data replication, consistency issues, etc. Managed clud services have alleviated this (you can use DynamoDB or MongoDB Atlas and not worry about the servers), but in a self-hosted scenario, NoSQL might require more effort to maintain.
	- A sharded SQL cluster can also be quite complex to maintain.
  - **Polyglot persistence**: Modern architectures might use both SQL and NoSQL for different parts of a system.
    - Example: Use SQL for the core business data (where consistence is crucial) and NoSQL for logging or caching or user session data. This requires knowing multiple systems, but many large systems are polyglot. Use the right tool for each job.
  - **Bottom line**: NoSQL offer more flexibility and speed during development since you're less constrained by schemas, which can be advantageous in fast-moving projects or when dealing with cutting-edge use cases. SQL offers a more structured environment that can prevent mistakes (e.g., you cannot accidentally insert a malformed record that breaks assumptions) and comes with a wealth of tools and knowledge in the industry. Consider you team's expertise and the project requirements. Often, starting with SQL is safe (especially if structure is clear), and introduce NoSQL components as needs arise (like scaling out reads with a caching layer, or using a document DB for a specific feature, etc.).

### Comparison table

| Aspect             | SQL DBs (Relational) | NoSQL (Non-relational) |
|:------------------:|:--------------------:|:----------------------:|
| Data model         | Relational (tables with rows and columns). Data is normalized into structured tables with defined relationships (foreign keys).                     | Variety of models (documented, key-value, column-family, graph, etc.) Data can be nested or denormalized, stored in flexible format (JSON, etc.).                       |
| Schema             | Fixed schema (must define tables and columns up front). Each row must adhere to the schema. Changing schema requires migration.                     | Dynamic schema (flexible/optional schema). Each record can have different fields. Easy to add new fields. Application logic handles interpretation.                       |
| Scalability        | Vertical scaling (add more hardware resources to the server) is the norm. Horizontal scaling (sharding) is possible but complex to implement for consistency.                     | Horizontal scaling (add more servers) is built-in for many NoSQL systems. Designed to distribute data across nodes, making it easier to scale to large data sizes or traffic volumes.                       |
| Consistency        | Strong consistency by default. Follows ACID transactions for reliable, all-or-nothing operations. Suited for use cases requiring up-to-date data and integrity (CP in CAP theorem).                     | Often eventual consistency for distributed setups. Many follow BASE (Basically Available, Soft state, Eventual consistency) for higher availability. Some can be tuned towards strong consistency at the cost of availability (AP in CAP, leaning towards availability).                       |
| Transactions       | Robust multi-step transactions supported (commit/rollback). Ensures data integrity across multiple operations (important for financial systems, etc.).                     | Limited multi-document transaction support (varies by DB). Typically focused on single-record atomic operations. Some NoSQL (like MongoDB) added transaction support, but not as full-fledged or high-performance as SQL for complex transactions.                       |
| Query capabilities | Advanced SQL queries (`JOIN`s across tables, complex `WHERE` conditions, aggregations with `GROUP BY`, subqueries, etc.) are supported by the DB engine itself. Great for analytics and relational data exploration.                     | Limited join or complex query capabilities natively. Queries are usually simple lookups by key or simple filters on one collection. For complex queries, data often needs to be structured accordingly (denormalized), or handled in application code. Some have aggregation frameworks, but as SQL-rich.                       |
| Performance        | High performance for complex queries on moderate data sizes (leverages indexes and optimized query planners). Writes can be slower if complex transactions or constraints need checking. Vertical scaling can handle a lot, but at extreme scale might bottleneck without sharding.                     | High performance for simple queries and massive scale. Can handle high write and read throughputs by spreading load (e.g., millions of ops/sec in key-value stores). Performance on complex aggregations might require external processing or map-reduce style approaches. Low latency reads/writes achievable with in-memory or geographically distributed nodes.                       |
| Flexibility        | Rigid structure (changes are slow). Great for consistency, repeatable transactions but less adaptabel to change. Any new data requirement might need altering the schema and migration data.                     | Very flexible (can adapt to changes quickly. Supports agile development (store new kinds of data as needed). Suitable for varying or eveolving data models (e.g., user profiles with varying attributes).                       |
| Ecosystem & Tools  | Extremely mature (vast array of tools for administration, analytics (SQL works with many BI tools), ORMs, etc. Many developers skilled in SQL.                     | Still maturing. Tooling depends on specific DB (each NoSQL has its own ecosystem). Fewer universal standards (though JSON is common). Need specialized knowledge for some (Cassandra data modeling, MongoDB sharding, etc.). Improving rapidly, but expertise may be less common.                       |
| Use cases          | Best for structured, relational data, like financial systems, banking, e-commerce transactions, inventory, order management, user credentials, systems needing consistent state, and complex queries. Whenever data integrity and consistency are paramount. Also, situations where the data structure is well-understood and not likely to change often.                    | Best for large-scale or flexible data, like social media (posts, comments, likes across distributed users), real-time analytics and big data, content management with varied metadata, IoT sensor data, logs, caching user sessions, and other scenarios requiring scaling out and handling lots of unstructured or semi-structured data. Great when you need high availability across regions or have rapidly evolving schemas.                      |

### What to choose?

Choosing between SQL and NoSQL depends on your project's requirements. Neither SQL nor NoSQL are universally better, they are optimized for different things. The choice is driven by the specific needs of the application. In many cases, both can complement each other in a single system. Evaluate the trade-offs in the context of your system's unique requirements. Some guidelines are:

**Choose SQL if:**

- **Data is structured and relational**: Data fits nicely into tables with clear relationships. Example: An e-commerce application with customers, orders, products, etc., where you benefit from foreign keys and joins.
- **Consistency is critical**: You cannot tolerate even minor inconsistencies. Example: Financial transactions, inventory counts, booking systems (double booking a seat due to eventual consistency delay would be bad). SQL's ACID guarantees shine here.
- **Complex querying is needed**: You need to frequently query the data in complex ways (like joining multiple tables, doing analytics, or lots of different query patterns that aren't predetermined). SQL's flexibility in querying is very valuable in such cases.
- **Transactions are a core part of the workload**: Many multi-steps operations that must all succeed or fail together (bank transfers, order placements that involve multiple tables, etc.).
- **Long-term maintenance and Reporting**: System well-understood by engineers and analysts, with existing tools for reporting, backups, etc. SQL is a mature ecosystem.

**Choose NoSQL if:**

- **Massive scale or High throughput required**: Web-scale traffic or data volume that a single server cannot handle. NoSQL is more adept at scaling out. Example: Social network's feed, log aggregation system, or any service expecting millions of users and constant growth.
- **Flexible or Evolving data models**: Data that doesn't fit a strict schema or is constantly changing (like storing documents from different sources, user-generated content with varying fields, or rapidly adding new features that require new data attributes). NoSQL lets you adapt without migrations. Great for startup or projects where requirements aren't fully nailed down.
- **Low latency, High performance simple ops**: You mostly do simple operations but at a very high volume (like caching, session storage, or real-time analytics). NoSQL can be tuned for microsecond or millisecond read/writes by sacrificing other features. Example: Redis for caching, or Cassandra for time-series inserts.
- **Geographically distributed data**: Multi-region deployments with local read/writes in each region (to serve users around the world with low latency). Many NoSQL DBs handle replication and partitioning across data centers gracefully. Some SQL solutions do this too, but it's often easier to accomplish eventual consistency models in NoSQL for multi-region.
- **Specific data models fitting NoSQL**: Data that naturally fits a document, graph, or other NoSQL model better than a relational one. Example: a social network is more straightforward in a graph DB than in SQL tables with join tables for relationships.

**Use both:**

- **Polyglot persistence**: Using different data storage technologies for different parts of the system based on their strengths.
- Example: An online retail system might use SQL DB for transactions and inventory (for accuracy), but NoSQL DB to store user activity logs, or to power a recommendation engine that needs to sift through lots of semi-structured click data.

**Explain choices**:

- Tie the choice back to requirements: 
  - "We should use SQL DB here because we need strong consistency for financial data and the ability to do complex joins for reporting. The data model is well-defined and not likely to change often".
  - "We should use a NoSQL solution here because we expect to handle a huge volume of writes globally, and we can tolerate eventual consistency. The schema might evolve, and using a document store will let us iterate without downtime".
- Mention how you'll mitigate the downsides (show you understand the trade-offs):
  - "If we use SQL and it becomes a bottlenech, we can partition by user region to scale writes, and use caching to offload reads".
  - "If we use NoSQL and we need to do some analytics, we might export the data to a warehouse or use a separate service fro those queries."

### Hybrid approach example

Imagine a high-scale web application like a ride-sharing service (Uber-like):

- A **SQL DB** could be used for critical data (ride transactions, payments, user accounts…), things that require consistency (we don't want inconsistent payment records).
- A **NoSQL DB** (or multiple) can be used for other aspects: perhaps MongoDB or Cassandra cluster to store real-time ride location logs, driver pings, etc., which are high volume and can be eventually consistent. Or use Redis to cache surge pricing data or active drivers in an area for quick retrieval.
- Maybe use a **graph DB** to maintain the relationship network of drivers, riders, referrals, etc., if that became a complex domain.
- The system becomes polyglot (each component storing data in the way that best fits its access patterns. The trade-off is complexity in maintaining multiple systems, but it can be worth it at large scale.
- For many smaller projects, sticking to one primary DB is enough, but it's useful to know that mixing isn't uncommon.


## CAP theorem

In distributed systems, different types of failures can occur (servers can crash or fail permanently, disks can go bad resulting in data losses, network connection can be lost and make part of the system inaccessible, …).

**CAP theorem**: It's impossible for a distributed system to simultaneously provide all 3 of the following desirable properties:

- **Consistency (C)**: All nodes/users see the same data at the same time. Users can read or write from/to any node in the system and will receive the same data. It's equivalent to having a single up-to-date copy of the data.
- **Availability (A)**: The system remains accessible even if one or more nodes in the system go down. Every request received by a non-failing node in the system must result in a response. Even when severe network failures occur, every request must terminate.
- **Partition tolerance (P)**: The system continues to operate even if there're partitions in the system. Such a system can sustain any network failure that does not result in the failure of the entire network. Data is sufficiently replicated across combinations of nodes and networks to keep the system up through intermittent outages.
  - **Partition**: Communication break (or network failure) between any two nodes in the system (both nodes are up but cannot communicate with each other).

Thus, we have 3 options: C+A, C+P, A+P. However, C+A is not a coherent option, as a non-partition-tolerant system will be forced to give up either C or A in the case of a network partition. Therefore, the theorem can really be stated as: **In the presence of a network partition, a distributed system must choose either Consistency or Availability**.

DB examples:

- C+P: BigTable, HBase
- A+P: Dynamo, Cassandra, CouchDB
- C+A: RDBMS

Building a general data store requires choosing 2 of those properties. If it's consistent, all nodes should see the same set of updates in the same order. But if the network loses a partition, updates in one partition might not make it to the other partitions before a client reads from the out-of-date partition after having read from the up-to-date one. The only thing that can be done to cope with this is to stop serving requests from the out-of-data partition, but then the service is no longer 100% available.


## PACELC theorem

We cannot avoid partition in a distributed system, therefore, according to **CAP theorem**, we have to choose between consistency or availability.

- **ACID** (Atomicity, Consistency, Isolation, Durability) DBs, such as RDBMSs like MySQL, Oracle, and Microsoft SQL Server, chose consistency (refuse response if it cannot check with peers).
- **BASE** (Basically Available, Soft-state, Eventually consistent) DBs, such as NoSQL DBs like MongoDB, Cassandra, and Redis, chose availability (respond with local data without ensuring it's the latest with its peers).

CAP theorem doesn't explain the choices of a distributed system when there's no network partition (when we maintain high availability by replication). PACELC theorem solves this by extending the CAP theorem (PAC is the CAP theorem, ELC is the extension).

**PACELC theorem**: In a system that replicates data:

- if there's a partition (P), a distributed system can tradeoff between availability and consistency (A and C).
- else (E), when the system runs normally in the absence of partitions, the system can tradeoff between latency (L) and consistency (C).

Examples:

- **Dynamo** and **Cassandra** are PA/EL systems: They choose A over C when a partition occurs; otherwise, they choose lower L.
- **BigTable** and **HBase** are PC/EC systems: They always choose C, giving up A and lower L.
- **MongoDB** can be considered PA/EC (default configuration): It works in a primary/secondary configuration. In default configuration, all writes and reads are performed on the primary. As all replication is done asynchronously (from primary to secondaries), when there's a network partition in which primary is lost or becomes isolated on the minority side, there's a chance of losing data that is unreplicated to secondaries, hence there's a loss of consistency during partitions. Therefore, it chooses A when a partition occurs; otherwise, it guarantees C. Alternately, when it's configured to write on majority replicas and read from the primary, it could be categorized as PC/EC.


## Consistent hashing

### Background

When designing a scalable system, the most important aspect is defining how data will be partitioned and replicated across servers. A careful designed scheme for partitioning and replicating the data enhances the system's performance, availability, and reliability, and defines how efficiently the system will be scaled and managed.

- **Data partitioning**: Process of distributing data across a set of servers (nodes). It improves the system's scalability and performance.

- **Data replication**: Process of making multiple copies of data and storing them on different servers. It improves availability and durability of the data across the system.

**Consistent hashing** was introduced by David Karger et al. in their [1997 paper](https://dl.acm.org/doi/10.1145/258533.258660) and suggested its use in distributed caching. Later, it was adopted and enhanced to be used across many distributed systems.

### Data partitioning

There're two challenges when trying to distribute data:

- How do we know on which node a particular piece of data will be stored?
- When we add or remove nodes, how do we know what data will be moved from existing nodes to the new nodes? Additionally, how can we minimize data movement when nodes join or leave?

Hashing solution: Use a suitable hash function to map the data key to a number (`number`). Apply modulo to find the server (`number % num_servers`). Example: `key = "Texas"` → `hash(key) = 16` → `16 % num_servers = 17 % 5 = 2`.

Hashing solves the problem of finding a server for storing/retrieving data. But adding or removing a server breaks all our existing mappings because the total number of servers change, which was used to find a server. To solve this, we have to remap all the keys and move our data based on the new server count (a complete mess).

### Consistent hashing

**Consistent hashing** can be used in distributed systems to distribute data across nodes. It ensures that only a small set of keys move when servers are added or removed. It stores the data managed by a distributed system in a ring. The ring is divided into smaller, predefined ranges, and each node is assigned a range of data. The start of a range is called a **token**. Each node is assigned one token. A range starts at `token_value` and ends at `next_token_value - 1`.

Example: Consider 4 in total and a hash range [1, 100]. The number range per node is 100/4. Then, all data in range [1, 25] is stored in server 1, range [26, 50] in server 2, range [51, 75] in server 3, and range [76, 100] in server 4.

| Server  | Token | Range     |
|:-------:|:-----:|:---------:|
| 1       | 1     | [1, 25]   |
| 2       | 26    | [26, 50]  |
| 3       | 51    | [51, 75]  |
| 4       | 76    | [76, 100] |

To read or write data, the [MD5 hashing algorithm]() is applied to the key to determined within which range the data lies and hence, on which node the data will be stored.

- **MD5** (MD5 Message-Digest 5 Algorithm): Hashing function that accepts a message of any length as input and returns as output a fixed-length digest value.

Consistent hashing works well when a node is added or removed from the ring, since only the next node is affected (example: when a node is removed, the next node becomes responsible for all the keys stored on the outgoing node). However, this scheme can result in non-uniform data and load distribution. This can be solved using **Virtual nodes**.

### Virtual nodes

Adding and removing nodes in a distributed system that uses Consistent hashing is handled using virtual nodes (or Vnodes).

**Basic Consistent hashing** assigns a single token (a consecutive hash range) to each physical node. Tokens are calculated based on the number of nodes. This makes adding or replacing a node an expensive operation, as we would like to rebalance and distribute the data to all other nodes, resulting in moving a lot of data. Potential issues with a manual and fixed division of ranges:

- **Adding/removing nodes**: Results in recomputing tokens causing a significant administrative overhead for a large cluster.
- **Hotspots**: Since each node is assigned one large range, if the data is not evenly distributed, some nodes can become hotspots (a server responsible for a huge partition of data can become a bottleneck because it receives a large share of data storage and retrieval requests, which can bring the performance of the whole system down).
- **Node rebuilding**: Since each node's data might be replicated (for fault-tolerance) on a fixed number of other nodes, when we need to rebuild a node, only its replica nodes can provide the data. This puts a lot of pressure on the replica nodes and can lead to service degradation.

To handle these issues, instead of assigning a single token to a node, each physical node is assigned several smaller ranges (Vnodes) (the hash range is divided into multiple smaller ranges). Each node is responsible for many tokens (or subranges) instead of just one. Advantages of Vnodes:

- Vnodes help spread the load more evenly across the physical nodes on the cluster by dividing the hash ranges into smaller subranges, which speeds up rebalancing after **adding/removing nodes**. When adding a node, it receives many Vnodes from existing nodes to maintain a balanced cluster. When **rebuilding a node**, instead of getting data from a fixed number of replicas, many nodes participate in the rebuild process.
- Vnodes make it easier to maintain a cluster containing **heterogeneous machines** because we can assign a high number of subranges to a powerful server and a lower number to a less powerful server.
- Vnodes help assign smaller ranges to each physical node, which decreases the probability of **hotspots**.

### Data replication using Consistent hashing

To ensure **high availability** and **durability**, Consistent hashing replicates each data item on multiple N nodes in the system (N is equivalent to the replication factor).

- **Replication factor**: Number of nodes that will receive the copy of the same data. Example: if a replication factor is 2, there're 2 copies of each data item, each one on a different node.
- **Availability**: System's ability to perform its required function continuously without failing for a designated period of time.
- **Durability**: System's ability to prevent the loss of data that was successfully committed to it. Durability guarantees against any data loss due to corruption or a permanent component failure.

Each key is assigned to a **coordinator node** (generally the first node that falls in the hash range), which first stores the data locally and then replicates it to N-1 clockwise successor nodes on the ring. This results in each node owning the region of the ring between it and its Nth predecessor. In an **eventually consistent** system, this replication is done asynchronously (in the background), so copies of data don't always have to be identical as long as they are designed to eventually become consistent, which is used to achieve high availability.

### Overview

Consistent hashing helps with efficiently partitioning (scalability) and replicating data (availability). Amazon's [Dynamo](https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html) and Apache [Cassandra](https://en.wikipedia.org/wiki/Apache_Cassandra) use Consistent hashing to distributed and replicate data across nodes. Use case examples:

- System working with a set of storage (or database) servers that needs to scale up or down based on usage.
- Distributed system that needs dynamic adjustment of its cache usage by adding or removing cache servers based on the traffic load.
- System that wants to replicate its data shards to achieve high availability.


## Long-polling vs WebSockets vs Server-sent events

Long-Polling, WebSockets, and Server-Sent Events are popular **communication protocols** between a client (like a web browser) and a web server.

**HTTP protocol** (Hypertext Transfer Protocol): Application layer protocol in the Internet protocol suite. Foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources. It's a request-response protocol in the client-server model. A transaction starts with a client (like a web browser) submitting a request to a server (web server, hosting server…), which it attempts to satisfy and returns a response to the client describing the disposition of the request and optionally contains a requested resource. Standard HTTP web request:

1. A client opens a connection and requests data from the server.
2. The server calculates the response.
3. The server sends the response back to the client on the opened request.

### Ajax Polling

**AJAX** (Asynchronous JavaScript and XML): Web development technique that enables web applications to send and receive data from a server asynchronously, without requiring a full page reload. This allows for dynamic updates to specific parts of a webpage, improving responsiveness and user experience.

**Polling**: Standard technique used by most AJAX applications. The client repeatedly polls (or requests) a server for data. The client makes a request and waits for the server to respond with data. If no data is available, an empty response is returned.

- The client opens a connection and requests data from the server using regular HTTP.
- The requested webpage sends requests to the server at regular intervals (like 0.5 s).
- The server calculates the response and sends it back, just like regular HTTP traffic.
- The client repeats the above 3 steps periodically to get updates from the server.

Problem: The client has to keep asking the server for any ne data. This results in a lot of empty responses, creating HTTP overhead.

### HTTP Long-Polling

**Long-Polling** (or Hanging GET): Variation of the traditional polling. It allows the server to push data to a client whenever the data is available. The client requests data from the server like in normal polling, but expecting that the server may not respond immediately.

- If the server doesn't have any data available for the client, instead of sending an empty response, it holds the request and waits until some data becomes available.
- Once data is available, a full response is sent to the client. Then the client immediately re-requests data from the server so that the server will almost always have an available waiting request that it can use to deliver data in response to an event.

Basic life cycle of an application using HTTP Long-Polling:

1. The client makes an initial request using regular HTTP and then waits for a response.
2. The server delays its response until an update is available or a timeout has occurred.
3. When an update is available, the server sends a full response to the client.
4. The client typically sends a new long-poll request, either immediately upon receiving a response or after a pause to allow an acceptable latency period.
5. Each Long-Poll request has a timeout. The client has to reconnect periodically after the connection is closed due to timeouts.

### WebSockets

**Full-duplex (FDX)**: System allowing communication in both directions and simultaneously (unlike half-duplex). Example: telephones.

**WebSocket**: It provides [Full-duplex](https://en.wikipedia.org/wiki/Duplex_(telecommunications)#Full_duplex) communication channels over a single TCP connection. It provides a persistent connection between a client and a server that both parties can use to start sending data at any time. The client stablishes a WebSocket connection through a WebSocket handshake. If this process succeeds, then the server and client can exchange data in both directions at any time. This protocol enables communication between a client and server with lower overheads, facilitating real-time data transfer from and to the server. This is possible with a standardized way for the server to send content to the browser without being asked by the client and allowing for messages to be passed back and forth while keeping the connection open. This allows a two-way (bi-directional) ongoing conversation between client and server.

### Server-Sent Events (SSEs)

Under SSEs the client establishes a persistent and long-term connection with the server. The server uses this connection to send data to a client. If the client wants to send data to the server, it would require the use of another technology/protocol to do so.

1. Client requests data from a server using regular HTTP.
2. The requested webpage opens a connection to the server.
3. The server sends the data to the client whenever there's new information available.

SSEs are best when we need real-time traffic from the server to the client or if the server is generating data in a loop and will be sending multiple events to the client.


## Bloom filters

### Introduction

**Bloom filter**: Magical checklist that can answer questions of the form "Have we seen this item before?". It consists of 2 main components:

- **Bit array**: Array of bits, initially all set to 0.
- **Hash functions**: Several independent hash functions that each take an input item and produce and index (position in the bit array).

**Operations** on the Bloom filter:

- **Add an item**: The item is run through each hash function to get multiple array positions, and all the bits at all those positions are set to 1.
- **Query item** (check membership): The item is run through the hash functions to get the positions and check the bits.
  - If any one of those bits is 0, the item was definetely not in the set.
  - If all of those bits are 1, then the item is probably in the set (it could be a false positive).
  
Bloom filters **guarantee no false negative**. Any item added will have its bits set. But item that were never added might by coincidence have all their bits set by other items, leading the filter to erroneously report "probably present".

Using multiple hash functions spreads the influence of each item across the array. This redundancy makes false negative impossible: an item would have to lose all its bits to be missed, which can't happen unless we explicitly remove it. But if too many items crowd the same few positions, they can cause false positives by filling in all the bits for some item that wasn't added.

### How Bloom filters work

Consider 3 items (P, Q, R). Each item is hashed by 3 hash functions to specific positions in the bit array, which are then set to 1. To query a new item, you hash it and check the corresponding bit positions; if any required bit is 0, the item is definitely not in the set, but if all are 1 the item is probably in the set.

**Usage process**:

1. **Initialize**: Start with a bit array of length N, all bits set to 0. Decide on k independent hash function (each should output a number in range [0, N-1]).
2. **Adding an item**: Feed the item into each hash function to get k array indices. For each index, set the bit at that position in the array to 1.
3. **Querying a item**: Check if an element is in the set by running it through the same k hash functions to get k positions. Then check those positions in the bit array:
  - If any of those bits is 0, the item in not in the set.
  - If all k bits are 1, the item is possibly in the set. Either the item was added or those bits happened to be set by some other combination of items. There's a small chance that it's a false positive.
4. **Dealing with false positives**: If the filter answers "probably in the set", one usually double-checks via a slower method (like doing full lookup in a DB or cache) if exact confirmation is needed. The filter's job is mainly to screen out definitively missing items quickly, to avoid wasting time on costly lookups for items that aren't there.

These steps make Bloom filters extremely fast and memory-efficient. The time to add or check an item is O(k), where k is the number of hash functions (constant, independent of the number of stored elements). In practice, k is fixed and usually small (like 3 to 10), so Bloom filter operations take a fixed few hash computations and array accesses. This constant-time performance holds even when the set represented is huge (millions of items), which is a big advantage over structures like lists or trees for membership testing.

**Removing items**: Not supported in standard Bloom filters. Clearing a bit set to 1 could remove information about other items that hashed that bit. You can only add items or reset everything. Bloom filters are best suited for scenarios where the set only accumulates or where you can occasionally rebuild or refresh the filter if needed.

- There're variantes like **Counting Bloom filters** that use counters instead of single bits to allow deletions, but they use more memory and complexity.

### False positives

Bloom filters trade perfect accuracy for efficiency.

Once a bit is set to 1 for an added item, that bit remains set, ensuring no future query for that item will find a 0 and falsely conclude "not present". 

False positives happen because different items overlap in the bits they set. Sometimes, an unlucky combination of items can fill all the bits that a query item would require. The Bloom filter has no way to tell that those bits were set by other items, so it can only report "probably present". A Bloom filter compresses information about the set, which saves space, but loses the ability to distinguish some different combinations of items.

The probability of a false positive can be tuned by adjusting this:

- Size of the bit array (n): The bigger it is, the more sparsely bits are filled for the same number of items, reducing the chance of accidental overlaps.
- Number of hash functions (k): The bigger the number, the more bits are covered by each items, which can either increase or decrease false positives depending on balance (too few hashes and each item doesn't mark enough territory, too many and you fill the array too quickly).

There's an optimal k for a given n and number of items that minimizes false positives. Designers choose parameters so that false positive probability is very low (say 1% or 0.1% or even less) based on what's acceptable for the application. A clear trade-off is: more memory = fewer false positives. Many systems let you configure this trade-off (example: Apache Cassandra, a distributed DB, allows tuning the Bloom filter's target false-positive rate, using more RAM to get it as low as needed).

False positives are the price of massive space and time savings. In exchange for never missing a member and using very little memory, we accept a slim chance of getting a "maybe" for something that isn't really there. In scenarios where a false positive only causes a minor extra step (like unnecessary DB lookup), Bloom filters are a huge win.

## Quorum

In distributed systems, data is replicated across multiple servers for fault tolerance and high availability. However, how to make sure that all replicas are consistent? (i.e., that all have the latest copy of the data and all clients see the same data).

**Quorum**: Minimum number of server on which a distributed operation needs to be performed successfully before declaring the operation's success.

Consider a DB replicated on 5 machines. The quorum is the minimum number of machines that perform the same action (commit or abort) for a given transaction in order to decide the final operation for that transaction. Three machines form the majority quorum, and if they agree, we will commit that operation. Quorum enforces the consistency requirement needed for distributed operations.

In systems with multiple replicas, it's possible that users read inconsistent data (data that is behind the last update).

What value should we choose for a quorum? More than half of the number of nodes in the cluster: N/2 + 1 (where N = total number of nodes in the cluster).

- In a 5-node cluster, 3 nodes must be online to have a majority. The system can afford 2 node failures.
- In a 4-node cluster, 3 nodes must be online to have a majority. The system can afford 1 node failure.
- Thus, it's recommended to have an odd number of totla nodes in the cluster.

Quorum is achieved when nodes follow **R + W > N** (where N = nodes in the quorum group, W = minimum write nodes, R = minimum read nodes). If a distributed system follows this rule, every read will see at least one copy of the latest value written. Examples:

- N=3, W=2, R=2: Common configuration. Strong consistency.
- N=3, W=1, R=3: Fast write, slow read, not very durable.
- N=3, W=3, R=1: Slow write, fast read, durable.

Before deciding read/write quorum, keep in mind this:

- R=1, W=N: Full replication (write-all, read-one). Undesirable when servers can be unavailable because writes are not guaranteed to be complete.
- 1<R<W<N: Best performance (throughput/availability) because reads are more frequent than writes in most applications.

**How it works:**

- **Majority-based quorum**: Most common quorum type. An operation requires a majority (more than half) of the nodes to agree or participate. Example: in a system with 5 nodes, at least 3 must agree for a decision to be made.
- **Read and write quorums**: For read and write operations, different quorum sizes can be defined. Example: a system might require a write quorum of 4 nodes and a read quorum of 2 nodes in a 5-node cluster.

**Use cases:**

- **Distributed DBs**: Ensuring consistency in a DB cluster, where multiple nodes might hold copies of the same data.
- **Cluster management**: A quorum decides which nodes form the active cluster, especially important for avoiding "split-brain" scenarios where a cluster might be divided into two parts, each believing it's the active cluster.
- **Consensus protocols**: In algorithms like Paxos or Raft, a quorum is crucial for achieving consensus among distributed nodes regarding the state of the system or the outcome of an operation.

**Advantages:**

- **Fault tolerance**: Allows the system to tolerate a certain number of failures while still operating correctly.
- **Consistency**: Helps maintain data consistency across distributed nodes.
- **Availability**: Increases the availability of the system by allowing operations to proceed as long as the quorum conditions are met.

**Challenges:**

- **Network partitions**: In cases of network failures, forming a quorum might be challenging, impacting system availability.
- **Performance overhead**: Achieving a quorum, especially in large clusters, can introduce latency in decision-making processes.
- **Complexity**: Implementing and managing quorum-based systems can be complex, particularly in dynamic environments with frequent node or network changes.

Quorum is fundamental in distributed systems and crucial for ensuring consistency, reliability, and availability when multiple nodes work together. It enhances fault tolerance, but introduces additional complexity and requires careful design and management to balance consistency, availability, and performance.

## Leader and follower

Distributed systems keep multiple copies of data for fault tolerance and higher availability. A system can use quorum to ensure data consistency between replicas (i.e., all read and writes are not considered successful until a majority of nodes participate in the operation). However, using quorum can lead to lower availability (at any time, the system needs to ensure that at least a majority of replicas are up and available, otherwise the operation fails). Quorum is also not sufficient, as in certain failure scenarios, the client can still see inconsistent data.

The solution is to allow only a single server (**leader**) to be responsible for data replication and to coordinate work. At any time, one server is elected as the leader. It becomes responsible for data replication and can act as the central point for all coordination. The followers only accept writes from the leader and serve as a backup. In case the leader fails, one of the followers can become the leader. In some cases, the follower can serve read requests for load balancing.

![Client, leader and followers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_13.png)

The leader entertains requests from the client and is responsible for replicating and coordinating with followers.

## Heartbeat

In a distributed environment, work/data is distributed among servers. To efficiently route requests in such setup, servers need to know what other servers are part of the system, and if they're alive and working. In a decentralized system, whenever a request arrives at a server, the server should have enough information to decide which server is responsible for entertaining that request. This makes the timely detection of server failure an important task, which also enables the system to take corrective actions and move the data/work to another healthy server and stop the environment from further deterioration.

The solution is that each server periodically sends a heartbeat message to a central monitoring server or other servers in the system to show that it's still alive and functioning.

Heartbeating is one of the mechanisms for detecting failures in a distributed system. If there's a central server, all servers periodically send a hearthbeat message to it. If there is no central server, all servers randomly choose a set of servers and send them a heartbead message every few seconds. This way, if no heartbeat message is received from a server for a while, the system can suspect that the server might have crashed. If there's no heartbeat within a configured timeout period, the system can conclude that the server is not alive anymore and stop sending requests to it and start working on its replacement.

## Checksum

In a distributed system, while moving data between components, it's possible that the data fetched form a node may arrive corrupted. This corruption can occur because of faults in a storage device, network, software, etc. How can a distributed system ensure data integrity, so that the client receives an error instead of corrupt data?

The solution is to calculate a checksum and store it with the data. To calculate a checksum, a cryptographic hash function is used (like MD5, SHA-1, SHA-256, or SHA-512). The hash function takes the input data and produces a string (checksum) of fixed length, containing letters and numbers. When a system is storing some data, it computes a checksum of the data and stores the checksum with the data. When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.