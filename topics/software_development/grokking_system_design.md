# Grokking system design

## Table of Contents
+ [References](#references)
+ [Introduction](#introduction)
+ [Glosary](#glosary)
+ [Tradeoffs](#Tradeoffs)
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
- Security: How it protects sensitive data and resist unauthorized access.

**Integrating both requirements**: Given an scenario, identify both the functional (what the system should do) and non-functional (hwo the system should do it) requirements. Balance both requirements and design a system that meets its functional goals while performing effectively, securely, and reliably. How to handles these requirements:

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
- __Latency__: Response time and latency of the system based on its architectur and components.
- __Resource__: Number of servers, CPUs, or memory required to handle the load and maintain desirec performance levels.

**Process**:

- __Understand the scope__: Clarify the scale of the problem (how many users, how much data, …).
- __Use simple math__: Use basic arithmetic to estimate the scale of data and resources.
- __Round numbers for simplicity__: Use round numbers to make calculations easier and faster.
- __Be logical and reasonable__: Ensure your estimations make sense given the context of the problem.

**Estimation examples**:

- __Load: A social media platform has 100 million users/day, and an average of 100 posts/user/day. Estimate load: `(100,000,000 · 10) / 86,400 seconds/day ≈ 11,574 requests/second`.
- __Storage: A photo-sharing app has 500 million users, and an average of 2 photos uploaded by user per day, each photo with an average size of 2 MB. Estimate storage required for one day's worth of photos: `500,000,000 · 2 · 2 = 2,000,000 MB/day`.
- __Bandwidth__: A video streaming service has 10 million users streaming 1080p videos at 4 Mbps. Estimate required bandwidth: `10,000,000 · 4 = 40,000,000 Mbps`.
- __Latency__: An API fetches data from source A, B, and C, with an average latency for each source of 50 ms, 100 ms, and 200 ms, respectively. Estimate total latency: `50 + 100 + 200 = 350 ms`. If the data fetching process is parallel, the total latency is the maximum latency among the sources: `max(50, 100, 200) = 200 ms`.
- __Resource__: A web application receives 10,000 request/second, each one requiring 10 ms of CPU time. Estimate total CPU time/second: `10,000 · 10 = 100,000 ms/second`. Estimate number of required CPUs, assuming each CPU core can handle 1,000 ms of processing per second: `100,000 / 1000 = 100 cores`.

**System design examples**: Estimate the system requirements for the following design examples. By breaking down the problem into smaller components, applying estimation techniques, and aggregating the individual estimates, you can derive a rough idea of the system's requirements, which can guide your design choices and resource allocation.

- **Messaging service** (similar to WhatsApp):
  
  - __Total number of users__: Based on market research, competitor analysis, or historical data.
  - __Messages per user per day__: Average. Based on user behavior patterns or industry benchmarks.
  - __Message size__: Average. Consider text, images, videos, and other media content.
  - __Storage requirements__: Total storage needed to store messages for a specified retention period. Consider number of users, messages per user, message size, and data redundancy.
  - __Bandwidth requirements__: Bandwidth needed to handle the message traffic between users. Consider number of users, messager per user, and message size.

- **Video streaming platform** (similar to Netflix): 

  - __Total number of users__: Based on market research, competitor analysis, or historical data.
  - __Concurrent user__: Number of users streaming videos simultaneously during peak hours.
  - __Video size and bit-rate__: Average. Consider various resolutions and encoding formats.
  - __Storage requirements__: For storing the video content. Consider number of videos, their sizes, and data redundancy.
  - __Bandwidth requirements__: For handling the video streaming traffic. Consider number of concurrent users, video bit-rates, and user locations.

** Tips for estimations**:

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
  - It's ok not to konw everything. Be open about what you're unsure of to prevent providing incorrect information.


## Glosary

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

For full scalability and redundancy, we can try to balance load at each system's layer. We can add LBs at 3 places:

- Between user and web server.
- Between web servers and internal platform layer (like application servers or cache servers).
- Between internal platform layer and database.

[flow image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_2.png)

test

<br>![flow image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/system_design_2.png)








## Tradeoffs




## Problems