# Operating systems 1

<br>![computer systems image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_systems.jpg)

## Table of Contents
+ [Introduction to Operating Systems](#introduction-to-operating-systems)
+ [Process management & CPU scheduling](#process-management-&-cpu-scheduling)
+ [Concurrency](#concurrency)
+ [Memory management](#memory-management)
+ [Storage management and Shell scripting](#storage-management-and-shell-scripting)
+ [Input/Output management](#input-output-management)
+ [Security and Protection](#security-and-protection)
+ [Advanced topics and Case studies](#advanced-topics-and-case-studies)

## Introduction to Operating Systems**

**Operating systems (OSs) evolution**:

- **1st generation (40s-50s)**: Pre-OS machines. The earliest electronic computers had no operating systems. Programs were entered manually using switches, plugboards, or punched cards, and machines ran one job at a time. Vacuum tubes, very slow I/O, and long setup times meant little automation and no resource sharing, scheduling, or memory management.
- **2nd generation (50s-60s)**: Batch processing. This era introduced the first monitor programs, precursors to OS kernels. Jobs were grouped into batches and executed sequentially without user interaction. Transistors replaced vacuum tubes, and tape/disk storage enabled job queues. Early OS features included basic job scheduling, simple memory allocation, and primitive error handling.
- **3rd generation (60s-70s)**: Modern OS foundations. Major hardware and software innovations created the first modern OSs. Systems supported multiprogramming, allowing several programs in memory at once, and time-sharing, enabling many users to interact through terminals. New hardware features (interrupts, I/O channels, memory protection, and larger memory) allowed sophisticated capabilities such as process scheduling (round-robin, priority queues), virtual memory and paging, hierarchical file systems, and system calls and user-level security.
- **4th generation (80s-90s)**: Personal computers. With microprocessors and affordable RAM, operating systems became user-focused. GUIs such as Windows and macOS became standard, offering icons, windows, and menus. OSs supported: multitasking for consumer use, improved file systems (FAT, NTFS, HFS), and plug-and-play hardware detection. The OS evolved from a technical interface to a mainstream user tool.
- **5th generation (2000s-present)**: Distributed, mobile, and cloud OSs. Today’s OSs serve interconnected systems, mobile devices, and large data centers. Key areas include: distributed and cloud OSs (support large clusters, resource sharing, fault tolerance, and distributed file systems, while virtualization allows OSs to act as both host and guest via hypervisors, containers, and serverless frameworks), mobiles OSs (Android and iOS emphasize touch interfaces, strict sandboxing, power efficiency, and sensor integration), and modern desktop/server OSs (incorporate multi-core scalability, real-time scheduling, and advanced security such as ASLR, SELinux, and application sandboxing).

**Key components** of an OS's architecture:

- **Kernel**: The kernel runs in privileged mode and directly manages hardware. Core responsibilities include process control, memory management, interrupt handling, device management, and security enforcement.
- **System calls / OS interface**: System calls form the boundary between user programs and the kernel, allowing controlled access to file I/O, networking, process creation, and more.
- **Process management**: Handles process creation, scheduling, termination, context switching, and inter-process communication (IPC). Ensures efficient use of CPU resources.
- **Memory management**: Tracks RAM usage, handles allocation, segmentation, paging, and virtual memory while enforcing process isolation.
- **File system**: Provides logical file/directory structures, metadata, permissions, and ensures persistent storage.
- **Device drivers**: Interface between the OS and hardware devices by translating OS commands into device-specific operations. They abstract hardware details from applications.
- **I/O management**: Coordinates data transfer between CPU and devices, handles device queues, buffering, and DMA operations.
- **User interface (CLI/GUI)**: Allows users to interact with the system through commands or graphical elements.
- **Security and protection**: Includes user authentication, access control, encryption, auditing, and enforcing privilege boundaries.
- **Network subsystem**: Implements networking protocols, manages interfaces, and supports distributed and client/server applications.

**Types of OS**:

- **Monolithic OS** (Linux, Unix): All major services run inside one large kernel. Components call each other directly, enabling high performance but less fault isolation. Example: reading a file triggers a system call that directly invokes filesystem and driver code within the kernel.
- **Microkernel OS** (Mach, Minix 3, QNX): Only essential functions run in the kernel; filesystem, networking, and drivers run as user-space services. Communication uses message passing, increasing modularity and security. Failure in one service doesn’t crash the whole OS.
- **Layered OS**: Functions are divided into layers, each relying only on layers below. This improves clarity and debugging but limits flexibility.
- **Modular/Hybrid OS** (Windows, macOS, Linux): A core kernel provides essential services while drivers and subsystems load as modules. Balances performance with flexibility. Example: Windows dynamically loads driver modules when applications request file or network operations.
- **Distributed OS**: Multiple machines function as one system. Components like the file system or memory management may span multiple hosts, using network protocols to synchronize and provide transparency.
- **Mobile OS** (iOS, Android): Apps interact primarily with frameworks, and subsystems enforce strict sandboxing. The kernel handles low-level scheduling and drivers optimized for power efficiency and sensors.

## Process management & CPU scheduling**

**Single-threaded model**: It processes one task at a time, so delays in any operation slow down the entire system.

**Multithreading**: Different threads can handle different operations simultaneously. It improves responsiveness and concurrency, makes better use of CPU time (if one thread blocks, others continue running), and isolates tasks (errors in one module do not freeze the whole system).

**Context switching**: It allows the CPU to pause one thread and resume another by saving and restoring process/thread state (registers, program counter, memory mapping). It ensures fairness between tasks (no thread monopolizes the CPU), handles mixed workloads (ensures smooth progress of different tasks), provides real-time responsiveness (OS can immediately run high-priority tasks), supports fault confinement (if one thread misbehaves, the OS can pre-empt it, maintaining system stability), and enables controlled multitasking.

**Scheduling algorithms**:

- **Non-pre-emptive scheduling**: A running process keeps the CPU until it finishes or voluntarily releases it. Impact: 
  - No overhead of frequent context switches.
  - Predictable execution.
  - Critical tasks wait too long.
  - System becomes unresponsive when long tasks dominate.
- **Pre-emptive scheduling**: The OS interrupts a running process to give the CPU to a more urgent task. Impact:
  - Higher overhead from context switching.
  - High responsiveness for urgent tasks.
  - Better for systems with real-time constraints.
  - Prevents long tasks from blocking critical operations.
  - Complex priority design required (risk of starvation).

## Concurrency**

**Critical section**: Segment of code where shared data is accessed or modified.

**Semaphore**: Signaling mechanism used to control access to shared resources. A binary semaphore (0, 1) can guard access to a resource. When a process wants to access a resource, it performs a Wait operation. Only one thread can decrease the semaphore from 1 to 0. After completing the critical section, the thread performs a Signal operation, increasing the semaphore back to 1. This prevents multiple processes from accessing the same account concurrently, and controls access even if processes are scheduled unpredictably.

**Mutex** (mutual exclusion lock): It allows only one thread to lock it at a time. It's stronger and more rigidly defined than a semaphore for mutual exclusion only. A thread locks the mutex before entering the critical section, which prevents any other thread from locking the same mutex until it's released, and when the process finishes, it unlocks the mutex. Mutexes are ideal for shared objects that must never be accessed concurrently, and for operations that require strong ownership (only the locking thread may unlock the mutex).

If **synchronization fails**, the system becomes vulnerable to different issues:

- **Race conditions**: Without proper synchronization, two or more processes may execute the critical section simultaneously.
- **Lost updates**: One process’ update overwrites another’s, causing discrepancies.
- **Deadlocks**: Two processes wait indefinitely for resources (e.g., locks) held by each other. This only happens when a circular wait exists, and when a process holds some resources while waiting for others.
- **Inconsistent transaction reports: If synchronization fails, statements may show incorrect balances.
- **System crashes and Unrecoverable errors**: If multiple threads modify the same memory area, the system may enter a corrupted state.

**Deadlock prevention techniques**: Two common techniques are:

- **Resource Ordering (or Hierarchical Ordering)**: Assign a fixed global order to all resources (example: CPU > Memory > Storage). Every task must request resources in increasing order of this hierarchy. A process cannot request a lower-order resource while holding a higher-order one. By enforcing a fixed global order, circular waiting is impossible. Processes can hold resources but cannot form a cycle, so the system remains deadlock-free.
- **Hold and Wait Elimination**: Require processes to request all needed resources at once, before execution begins. If all resources are unavailable, the process waits without holding any resources. This eliminates the "hold and wait" condition, another necessary condition for deadlocks. By forcing a process to request all resources at once, a process either gets all resources or none. This ensures that no process holds partial resources while waiting, breaking one of the four Coffman conditions for deadlock.

**Deadlock avoidance vs prevention**:

- **Prevention**: Safe but conservative. It's simpler to implement, and guarantees deadlock-free operation. However, it can reduce resource utilization due to rigid rules, and may cause unnecessary delays if tasks could have executed safely.
  - Approach: Proactively constrains resource requests to prevent deadlocks (e.g., no hold-and-wait, no circular wait).
  - Resource allocation: Simple rules (ordering, hold-and-wait elimination).
  - Flexibility: Less flexible: some requests may be denied unnecessarily.
  - Complexity: Low (static rules, easy to implement).
  - Performance: Can underutilize resources (tasks wait longer).
- **Avoidance**: Efficient but complex. It makes efficient use of resource, and grants requests more flexibly, improving system throughput. However, it's computationally expensive (it tracks resources, allocation, and future requests), and is complex to implement for large HPC clusters with thousands of tasks.
  - Approach: Allows dynamic requests but ensures safe states before granting resources (like the Banker's Algorithm).
  - Resource allocation: Dynamic checks for safe states at runtime.
  - Flexibility: More flexible (grants requests if they keep system in a safe state).
  - Complexity: High (requires tracking all current allocations and future requests).
  - Performance: Better utilization (grants resources more aggressively while avoiding unsafe states).

The choice depends on whether predictable deadlock-free operation or maximum resource utilization is more critical. Often, a hybrid approach is used (prevention rules for critical resources, avoidance for flexible allocation of less critical resources).

## Memory management**

Different **memory management systems** manage memory very differently, which affects fragmentation, flexibility, and overhead.

- **Paging**: It divides memory into fixed-size frames (like 4 KB).
  - Advantages:
    - No external fragmentation: Any free frame can store a page, memory is used very evenly.
	- Easy to allocate: Suitable for many small data streams like sensor readings arriving every few milliseconds.
	- Predictable performance: Real-time systems benefit from predictable allocation and lookup times.
  - Disadvantages:
    - Internal fragmentation because a page is fixed-sized (a 500-byte log entry occupies a full 4 KB frame).
    - Large page tables may be required because the system handles many small streams.

- **Segmentation**: It divides memory into variable-sized segments depending on logical units (like “Critical Alerts Segment” and “Performance Logs Segment”).
  - Advantages:
    - No internal fragmentation: Segments match the data size closely.
	- Good when data streams have different lengths and purposes.
  - Disadvantages:
    - External fragmentation: Over time, free memory breaks into small holes as segments are allocated and deallocated at different sizes.
    - Segment sizes can fluctuate unpredictably due to real-time sensor variations.
	- Harder to manage when hundreds of variable-sized streams run simultaneously.

A hybrid approach is sometimes used (segmentation for high-level organization, and paging for each segment), though paging remains the core allocation technique.

**Demand paging**: Virtual memory mechanism in which pages of a process are loaded into physical memory only when they are actually needed, not at process startup. This reduces initial memory requirements and allows the system to run programs that exceed the size of physical RAM. This approach enables efficient memory usage while still giving each process the illusion of having large contiguous memory.

- Steps:
  1. Page referenced: The application tries to access a page that is not in physical memory.
  2. Page fault occurs: The Memory Management Unit (MMU) detects the missing page and triggers a trap to the OS.
  3. OS intervenes: The OS locates the required page in secondary storage (usually disk), selects a physical frame (possibly evicting another page), and loads the requested page.
  4. Page table updated: The process’s page table entry is updated to mark the page as valid.
  5. Execution resumes: The application continues as if the page had always been present.
  
- Advantages:
  - Reduced initial memory load: Only required pages are loaded, saving physical memory for other applications.
  - Better scalability and consolidation: The system can run more applications concurrently because not all pages must reside in memory.
  - Adaptive memory usage: When memory demand spikes, demand paging allows the OS to load only the newly needed pages.
  
- Disadvantages:
  - Increased page faults during high-demand periods: Variable workloads may cause bursts of page faults as the application touches new regions of memory.
  - Higher latency for first-time access: Accessing an uncached page involves disk I/O, which is significantly slower than RAM.
  - Risk of thrashing: If working set size grows beyond available RAM, the system may enter a state of constantly loading and evicting pages.

**Page replacement algorithms**: 

- **FIFO (First In, First Out)**: Evicts the page that has been in memory the longest. It may remove heavily used pages simply because they are old. It performs poorly under variable access patterns. It’s vulnerable to Belady’s Anomaly, where more frames can actually increase faults. FIFO is not ideal for the scenario since it’s inconsistent and often inefficient.
- **LRU (Least Recently Used)**: Evicts the page that has not been used for the longest time. It typically has lower page faults than FIFO. It adapts well when the application has locality (temporal and spatial). It performs better in scenarios where memory demand fluctuates but recent history is a good predictor. LRU is a strong candidate since it works well when data access patterns follow locality of reference.
- **Optimal (OPT) algorithm**: Evicts the page that will not be used for the longest time in the future. It produces the lowest possible page fault rate. It’s ideal for theoretical analysis but impractical because future memory references are unknown. It’s useful as a benchmark only, but cannot be implemented in real systems.
- **Clock (second-chance) algorithm**: Uses a circular buffer and reference bits to give pages a “second chance” before eviction. It approximates LRU at a lower cost. It performs moderately well for fluctuating workloads. More efficient in overhead than true LRU. It’s preferable for real-time or cloud systems that need a balance between performance and overhead.

## Storage management and Shell scripting**

**Directory structure**:

- **Flat directory**: It provides simple design (all files stored in one directory), easy navigation (no directory traversal needed), quick setup (minimal planning required), and is suitable for small systems (works well with few files). However, it has poor scalability (becomes unmanageable as file count grows), name conflicts (multiple files may require complex naming schemes), no logical grouping (hard to distinguish papers from datasets), and limited access control (permissions must be set per file).

- **Hierarchical structure**: It provides better organization (files are grouped logically), scalability (new projects or datasets can be added without disrupting existing files), efficient access control (permissions can be applied at directory levels), and easier file management (simplifies searching, backups, and maintenance), including and maintainability (easier backups, archiving, and collaboration). However, it has more complex navigation (users may need to traverse multiple directories), longer path names (increases path complexity), initial design effort (requires planning to avoid poor structure), and risk of deep nesting (over-nesting can reduce usability).

**Automation scripts**: Command-lines scripts used for automating daily backups, log management, disk monitoring, etc. 

Operational challenges:

- **Security and Access Control**: Scripts often require elevated privileges to access sensitive data and system directories. Poorly secured scripts can expose credentials or allow unauthorized access.
- **Reliability and Error Handling**: Scripts must detect and handle failures (like failed backup, network outage, insufficient disk space). Lack of proper logging or error handling could result in silent data loss.
- **Scheduling and Resource Contention**: Automation tasks often run during off-peak hours but still compete for I/O resources. Poor scheduling can interfere with some processes.
- **Scalability and Maintenance**: Scripts must scale across multiple servers with different configurations. Hard-coded paths or server-specific logic reduce maintainability.
- **Performance impact**: Disk-intensive scripts (backups, log movement) can degrade system performance. Throttling and prioritization are needed to avoid overwhelming the disk subsystem.

**Scheduling algorithms**: 

- **FCFS** (First-Come, First-Served): Disk I/O requests are serviced strictly in arrival order. It causes excessive disk head movement. It leads to high average seek time. The performance degrades badly under heavy transaction loads. It's simple and fair, but it has high seek time and poor performance.
- **SSTF**: Low average seek time, but it starve requests in low-traffic disk regions.
- **SCAN (Elevator)**: Balanced performance, though edge requests may wait longer. It improves over FCFS but still favors middle tracks.
- **C-SCAN** (Circular SCAN): It moves the disk head in one direction only (like outer to inner tracks). It services all requests in that direction. Upon reaching the end, it returns to the beginning without servicing requests during the return. It provides uniform wait times (critical for transaction fairness), reduces seek-time variability under heavy loads, ensures predictable performance, and is well-suited for high-volume, continuous disk access, though it has slightly more movement.

## Input/Output management**

**Prioritization strategies**: Used for managing concurrent inputs efficiently and reliably while ensuring important information is handled with the highest priority. Some strategies are:

  - **Priority-based interrupts**: Assigning higher interrupt priorities to some data ensures that it pre-empts routine input.
  - **Real-time scheduling policies**: This guarantees that critical tasks meet strict deadlines (example: processing immediately some important data).
  - **Separate data queues**: Important and unimportant data are placed in separate queues. Important data us processed first, while unimportant data can be handled later.
  - **Pre-emptive processing**: If important data comes in, the system can interrupt lower-priority tasks to process it.

**Device drivers**: Essential software components that allow the operating system to communicate with the hardware. They allow seamless communication, reliable data transfer, and effective error handling. Some features are:

  - **Hardware abstraction**: Drivers hide device-specific details and provide a uniform interface to the OS, allowing applications access devices without understanding their internal workings.
  - **Device initialization and configuration**: Drivers handle device setup during system startup, ensuring that each device is properly configured and ready for operation.
  - **Data transfer management**: Drivers manage how data is sent and received, including buffering, synchronization, and error detection. This ensures reliable and accurate data flow from devices.
  - **Error handling and recovery**: If a device malfunctions or communication fails, drivers detect errors and attempt recovery, preventing system crashes and data corruption.
  - **Security and access control**: Drivers enforce access restrictions, ensuring that only authorized processes can interact with critical medical equipment.
	
## Security and Protection

**Malware**: Software that contributes to data compromise and operational disruption. Some types are:

  - **Phishing-based trojans**: Phishing emails often deliver Trojan malware disguised as legitimate attachments/links. Once executed, they create backdoors that allow attackers to gain unauthorized access to a systems. They exploit human vulnerabilities (like lack of security awareness) and system vulnerabilities (like outdated email filtering and weak authentication controls).
  - **Ransomware**: It encrypts critical data and system files, rendering them inaccessible, until a ransom is paid. It typically exploits unpatched OSs, weak access controls, or malicious links delivered via phishing emails.
  - **Spyware**: Spyware, including keyloggers, may be installed alongside Trojans to silently monitor user activity and capture sensitive information.

**Access control strategies**: A layered access control can apply many strategies.

  - **Role-Based Access Control (RBAC)**: Users should only have access to data and systems necessary for their job functions, reducing the attack surface.
  - **Multi-Factor Authentication (MFA)**: Requiring additional authentication factors significantly reduces the risk of credential theft.
  - **Least Privilege Principle**: Access rights should be minimized and reviewed regularly.

**Security policies and Enforcement**:

- **Regular Security Audits**: Periodic vulnerability assessments and penetration testing help identify weaknesses before attackers can exploit them.
- **Employee Security Training**: Continuous training programs should educate staff on phishing detection, secure password practices, and incident reporting.
- **Monitoring and Logging Systems**: Implement real-time intrusion detection and security information and event management (SIEM) systems to monitor suspicious activity and enable rapid incident response.

**Encryption**: It can reduce the impact of ransomware attacks when implemented proactively. While ransomware uses encryption maliciously, defensive encryption prevents attackers from exploiting stolen data. Combined with secure backups and access controls, encryption minimizes data exposure and ensures faster recovery.

- **Data encryption for protection**:
  - Encryption **at Rest**: Encrypting stored data ensures that even if attackers gain access, the data remains unreadable.
  - Encryption **in Transit**: Protects sensitive data exchanged between systems from interception or tampering.

- **Traditional cryptographic approaches**: They often focus solely on protecting data confidentiality during storage or transmission.

- **Modern encryption strategies**:
  - **Key Management Systems (KMS)**: Secure handling and rotation of encryption keys.
  - **Backup encryption**: Ensuring encrypted, offline backups are available for recovery without paying ransom.
  - **Zero trust architectures**: Encryption is applied continuously, regardless of network location.

## Advanced topics and Case studies

**Systems localization**: 

- **Centralized system**: 
  1. It runs on a single logical machine with shared memory and a single point of control.
  2. Failures are usually total and obvious.
  3. It typically provides strong consistency with minimal coordination.
  4. It scales vertically (more CPU/RAM on one machine).
  5. It relies on local locks and shared memory.
  6. Smaller attack surface.
  
- **Distributed system**: It trades simplicity and low latency for scalability, fault tolerance, and resilience. Performance is often lower per operation, but overall system throughput and availability scale far beyond what centralized systems can support.
  1. It consists of multiple independent nodes communicating over a network. Network communication introduces latency, partial failures, and message loss, so application design must explicitly handle these conditions.
  2. Failures are partial (nodes, links, or services can fail independently). Fault tolerance mechanisms (replication, retries, consensus) add overhead but improve availability and resilience.
  3. It must balance consistency, availability, and partition tolerance (CAP theorem). Strict consistency often reduces performance and scalability due to coordination and synchronization costs.
  4. It scales horizontally (add more nodes), which enables much higher throughput and capacity, but requires data partitioning, load balancing, and coordination logic.
  5. It relies on message passing and distributed coordination protocols. Coordination increases latency and complexity, affecting performance under high contention.
  6. Big attack surface (it communicates over networks and across trust boundaries). Encryption, authentication, and authorization are mandatory, adding computational and operational overhead.

**Cloud computing and Virtualization**: They transform OSs into dynamic resource managers. This lowers costs, increases agility, and improves operational efficiency while maintaining performance and reliability.

- **Abstraction of hardware**: Both decouple applications from physical hardware through hypervisors and containers. CPUs, memory, storage, and networking are exposed as virtual resources. And OSs manage virtualized resources rather than fixed hardware. Resources can be allocated, resized, or reclaimed dynamically, improving utilization and flexibility.
- **Elastic and on-demand provisioning**: Modern OSs integrate with cloud control planes to support rapid provisioning and scaling. Virtual machines and containers can be created or destroyed in seconds. Auto-scaling policies respond to workload demand. Systems avoid over-provisioning while maintaining performance during peak loads.
- **Improved isolation and multi-tenancy**: Virtualization enforces strong isolation between workloads. Faults and performance issues are contained. Different tenants or applications safely share infrastructure. Higher consolidation ratios reduce infrastructure costs without compromising stability or security.
- **Resource-aware scheduling**: Cloud-aware OS schedulers optimize CPU, memory, and I/O allocation across virtualized workloads. This influences on CPU pinning, NUMA awareness, cgroups, quotas, and priority-based and workload-specific scheduling. Better performance predictability and reduced contention improve application reliability.
- **Automation and orchestration**: Operating systems increasingly work alongside orchestration platforms (e.g., Kubernetes). This influences on declarative resource specifications, automated placement, recovery, and updates. Operational overhead is reduced, enabling faster deployment cycles and consistent environments. Impact: cost efficiency (pay-as-you-go models and higher utilization lower capital and operating expenses), scalability (businesses scale infrastructure in line with demand, supporting growth without major upfront investment), agility (faster provisioning accelerates development, testing, and time-to-market), and reliability (built-in redundancy and automated recovery improve service availability).

**Linux**: OS originated in early 1990s as a Unix-like, monolithic kernel focused on stability, multi-user support, and portability across hardware. It has evolved from a simple Unix-like kernel into a highly scalable, secure, and versatile OS. Continuous adaptation has positioned Linux as the backbone of cloud computing, enterprise systems, and modern software delivery.

Key evolutionary changes:

- **Modular kernel architecture**: Over time, extensive support for loadable kernel modules was introduced. Also, drivers and subsystems can be loaded/unloaded at runtime. Moreover, the need for kernel recompilation was reduced. All this improved hardware compatibility, easier maintenance, and faster adoption across diverse platforms.
- **Scalability and performance enhancements**: Linux evolved to support symmetric multiprocessing (SMP), NUMA-aware scheduling, advanced I/O schedulers, and control groups (cgroups). All this made Linux suitable for everything from embedded devices to high-performance computing clusters and hyperscale data centers.
- **Security advancements**: Major security improvements include Mandatory Access Control (SELinux, AppArmor), secure namespaces and containers, and kernel hardening and sandboxing mechanisms. All this made Linux a trusted platform for multi-tenant environments, cloud computing, and regulated industries.
- **Virtualization and container support**: Linux incorporated first-class support for KVM (Kernel-based Virtual Machine), namespaces and cgroups (foundation of containers), and overlay and copy-on-write filesystems. All this made Linux the dominant OS for virtualization, containers, and cloud-native workloads.
- **Improved usability and ecosystem growth**: While the kernel remained technical, distributions evolved to address usability: package managers (APT, YUM, DNF), desktop environments (GNOME, KDE), and installer and configuration improvements. All this lowered the barrier to entry for developers, enterprises, and end users.

All this have influenced Linux functionality and market position:

- **Current functionality**: Today, Linux offers high reliability and uptime, strong security isolation, excellent performance under concurrent workloads, and unmatched flexibility through customization. Its design enables rapid adaptation to emerging technologies such as edge computing, IoT, and AI workloads.
- **Market position**: Linux currently dominates cloud infrastructure and container platforms, powers the majority of servers, supercomputers, and embedded systems, and serves as the foundation for Android and many commercial operating systems. While desktop market share remains modest, Linux’s strategic importance is extremely high due to its role in modern computing infrastructure.
