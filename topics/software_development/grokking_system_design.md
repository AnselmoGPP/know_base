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
+ [Problems](#problems)


## References
- [Grokking the system design interview](https://www.designgurus.io/course/grokking-the-system-design-interview?aff=84Y9hP)


## Introduction

### System design interview

**Purpose of system design interviews**: Assess a candidate's ability to design and understand complex and large-scale software systems. Assess whether you can apply engineering knowledge to real-world system architecture challenges. These questions are open-ended, there isn't a single correct answer. The emphasis is on the approach and reasoning behind the design. The goal is to evaluate how you think through large-scale problems and make engineering decisions. It's crucial for roles involving software systems and architectures (software engineer, system architect, DevOps engineer…). Key purposes are:

- __Assessing problem-solving skills__: How you approach and navigate complex, ambiguous problems. How you break them down, work towards a solution, and figure out a viable system design.
- __Evaluating technical knowledge__: Understanding of various system architecture components (databases, APIs, caching, load balancing, network protocols…), and how different pieces of a large system fit together.
- __Considering scalabitily, reliability, and maintainability__: How your design can handle growth (more user and data) and remain stable and performant over time.
- __Tradeoff analysis and decision-making__: There're many possible system designs. Why you choose a certain approach? Demonstrate great decision-making in balancing factors (performance, complexity, cost…).
- __Communication and collaboration__: Good communication is essential for explaining your design, answering questions, drawing diagrams, and collaborating with teammates.

### Functional vs. Non-functional requirements

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

### Back-of-the-envelope estimations

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

- **Sanity check**: Quick evaluation of an estimate to ensure its plausibility and reasonableness. This helps identify potentia errors or oversights in the estimation process and can lead to more accurate and reliable results. Example: comparing the estimated storage requirements for a messaging service with the actual storage used by a similar existing service can help validate the estimate.

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

### Things to avoid

A system design interview is not just about getting the right answer, but about demonstrating your problem-solving approach, ability to adapt, and communication and collaboration skills.

- **Don't ignore the Requirements**
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

### System design basics

When designing a large system, we need to consider:

- What are the different architectural pieces that can be used?
- How do these pieces work with each other?
- How can we best utilize these pieces? What are the right tradeoffs?

Investing in scaling before it's needed is generally not a smart business proposition. However, some forethought into the design can save valuable time and resources in the future.

### Key characteristics of Distributed systems

Key characteristics of a distributed system include: Scalability, Reliability, Availability, Efficiency, and Manageability.

#### Scalability

Capacity of a system/process/network to grow and manage increased demand. An scalable system can continuously evolve in order to support a growing amount of work. A system would like to achieve scaling without performance loss.

- There're many __reasons for scaling a system__: Increased data volume, increased amount of work (like number of transactions), etc.
- Generally, the __performance__ of a system, although designed to be scalable, declines with the system size due to the management or environment cost (example: network speed become slower because machines tend to be far apart from one another). Some tasks may not be distributed, due to their inherent atomic nature or to some flaw in the system design. At some point, such tasks would limit the speed-up obtained by distribution. A scalable architecture avoids this situation and attempts to balance the load on all the participating nodes evenly.
- __Scaling types__:
  - __Horizontal__: Scaling by adding more servers into your pool of resources. This is often easier for scaling dynamically. Examples: MongoDB, Cassandra.
  - __Vertical__: Scaling by adding more power (CPU, RAM, storage, …) to an existing server. This is usually limited by the capacity of a single server, and scaling beyond that capacity often involves downtime and comes with an upper limit. Example: MySQL.
  
![Scalability](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_1.png)

#### Reliability

Ability of a system to continue operating correctly and effectively in the presence of faults, errors, or failures. A reliable distributed system keeps delivering its services even when some software or hardware components fail, and any failing machine can always be replaced by a healthy one to ensure the completion of the task.

- __Example__: A large electronic commerce store, like Amazon, ensure that any user transaction is not canceled due to a failure of the machine running it. For instance, when the user adds items to his shopping cart, the system ensures that they are not lost by implementing redundancy of both software components and data (if the server fails, another one with a replica of the shopping cart replaces it). 
- Redundancy has a __cost__.
- __Reliability__ focuses on end-to-end correctness and consistency of the entire system's operation over time. It's primarily a user-centric concept (can the system consistently meet the user's expectations over time?). It' often measured in terms of _uptime_, _error rates_, _mean time between failures_ (MTBF).
- __Fault tolerance__: System's ability to continue operating (possibly at a reduced level) even when one or more of its components fail. It allows a system to absorb or recover from faults without total breakdown. It focuses on the system's ability to continue operating when individual components fail. It's more of a system-centric concept (how does the system handle internal failures or component breakdowns?). It's often measured by how quickly and effective the system detects, isolates and recovers from failures (like failover times).

#### Availability

Percentage of time a system/service/machine remains operational to perform its required function in a specific period, under normal conditions.

- __Example__: An aircraft with high availability can fly for many hours a month without much downtime. Availability takes into account maintainability, repair time, spares availability, and other logistics considerations. When it's down for maintenance, it's not available during that time.
- __Reliability__ is availability over time considering the full range of possible real-world conditions that can occur. An aircraft that can fly safely through any weather is more reliable than one with vulnerabilities to some conditions.
- A __reliable__ system is __available__ (high reliability contributes to high availability). But being available doesn't necessarily mean it's reliable. We can achieve high availability with an unreliable product by minimizing repair time and ensuring spares are always available when needed. Example: an online retail store has full availability for the first 2 years after launch, but the systems was launched with no information security testing so, though customers are happy, the system isn't very reliable since it has serious vulnerabilities. The 3rd year the system experiences some information security incidents that cause extremely low availability for extended periods of time, resulting in reputational and financial damage to the customers.

#### Efficiency

Assume we have an operation that runs in a distributed manner and delivers a set of items as a result. Two standard measures of its efficiency are:

- Response time (or latency): Delay to obtain the first item.
- Throughput (or bandwidth): Number of items delivered in a given time unit (second).

These correspond to two unit costs:

- Number of messages globally sent by the nodes of the system regardless of the message size.
- Size of messages representing the volume of data exchanges.

The complexityof operations supported by distributed data structures (like searching for a specific key in a distributed index) can be characterized as a function of one of these cost units. In general, analysing a distributed structure based on the number of messages is over-simplistic because it ignores the impact of many aspects (network topology, network load, its variation, heterogeneity of software and hardware components…). Since it's quite difficult to develop a precise cost model that accurately takes into account all these performance factors, we have to live with rough but robust estimates of the system behavior.

#### Manageability or Serviceability

How easy it is to operate and maintain the system. Simplicity and speed with which a system can be repaired or maintained. The longer it takes to fix a failed system, the lower availability it has. Things to consider are: ease of diagnosing and understanding problems when they occur, ease of making updates or modifications, and how simple the system is to operate (i.e., does it routinely operate without failure/exceptions?). Early detection of faults can decrease or avoid system downtime (example: some enterprise systems automatically call a service center when a system fault happens).

### Load balancing

**Load balancer (LB):** Important component of distributed systems. It helps spread traffic across a cluster of servers to improve responsiveness and availability of applications, websites or databases, and keeps track of the status of all resources while distributing requests. If a server is not available, or not responding, or has high error rate, LB will stop sending traffic to it. LB typically sits between client and server, accepting incoming network and application traffic and distributing traffic across multiple backend servers using various algorithms. By balancing application requrest across multiple servers, LB reduces individual server load and prevents any one application server from becoming a single point of failure, thus improving overall application availability and responsiveness.

![Load balancer](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_2.png)

For full scalability and redundancy, we can try to balance load at each system's layer. We can add LBs at 3 places:

- Between user and web server.
- Between web servers and internal platform layer (like application servers or cache servers).
- Between internal platform layer and database.

![Load balancer positions](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_3.png)

**Benefits of load balancing:**

- Users experience faster, uninterrupted service. No need to wait for a single struggling server to finish its previous task, since requests are immediately passed on to a more readily available resource.
- Service providers experience less downtime and higher throughput. Even a full server failure won't affect the end user expereince as the LB will route around it to a healthy server.
- Load balancing makes it easier for system administrators to handle incoming requests while decreasing wait time for users.
- Smart LBs provide benefits like predictive analytics that determine traffic bottlenecks before they happen. It gives an organization actionable insights, which are key to automation and can help drive business decisions.
- System administrators experience fewer failed or stressed components. Load balancing has several devices performing a little bit of work, instead of a single device performing a lot of work.

**Load balancing algorithms:**

Before forwarding a request to a backend server, a LB first ensures that the server they choose is actually responding appropriately to requests, and then use a pre-configured algorithm to select one from the set of healthy servers. Servers health is monitored through **health checks**: regular attempts to connect to servers to ensure that they are listening. A server that fails a health check is automatically removed from the pool, and traffic will not be forwardedto it until it responds to health checks again.

There're different load balancing algorithms for different needs:

- __Least connection method__: Directs trafic to the server with the fewest active connections. Useful when there're a large number of persisten client connections which are unevenly distributed between servers.
- __Least response time method__: Directs traffic to the server with the fewest active connections and the lowest average response time.
- __Least bandwidth method__: Selects the server that is currently serving the least amount of traffic measured in Mbps (megabits per second).
- __Round robin method__: Cycles through a list of servers and sends each new request to the next server. If the end of the list is reached, it starts over at the beginning. Useful when servers have equal specification and there're not many persistent connections.
- __Weighted round robin method__: Each server is assigned a weight (integer value indicating processing capacity). Servers with higher weights receive new connections before those with less weights, and servers with higher weights get more connections that those with less weights. This is designed to better handle servers with different processing capacities.
- __IP Hash__: A hash of the IP address of the client is calculated to redirect the request to a server.

**Redundant load balancers:** The LB can be a single point of failure. To overcome this, a second LB can be connected to the first to form a cluster. Each LB monitors the health of the other and, if the main LB fails, the second LB takes over.

![Redundant load balancers](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_4.png)

More about LBs:

- [What is load balancing](https://avinetworks.com/what-is-load-balancing/)
- [Introduction to architecting systems](https://lethain.com/introduction-to-architecting-systems-for-scale/)
- [Load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing))

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

### Data partitioning

**Data partitioning:** Process of dividing a large database (DB) into smaller, more manageable parts called **partitions** or **shards**. Each partition is independent and contains a subset of the overall data.






### Indexes
### Proxies
### Redundancy and Replication
### SQL vs. NoSQL
### CAP theorem
### PACELC theorem
### Consistent hashing
### Long-polling vs WebSockets vs Server-sent events
### Bloom filters
### Quorum
### Leader and follower
### Heartbeat
### Checksum






## Tradeoffs




## Problems