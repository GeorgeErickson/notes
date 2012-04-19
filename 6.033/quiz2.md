# Performance

## 6.1 Performance Metrics

-  **capacity** - a measure of a service's size
-  **utilization** - the percentage of capacity of a resource that is used
-  **overhead** - in a layered application its what the layers below it use
-  **useful work** - what is available to the application
  - e.g. if 10% of a disk is used for file system data structures then from the applications pov 10% is overhead of the fs and 90% is useful capacity
  
- **latency** 
  - low is good
  - delay between a change at the input to a system and the corresponding change at its output
  - **pipelining** - latency_a+b >= latency_a + latency_b

-  **throughput**
  - throughput <= Window / RTT  
  - the rate of useful work done by a service
  - throughput_a+b <= minimum(throughput_a, throughput_b)
  - when a stage processes request serially the throughput and the latency are directly related
    - throughput = 1 / latency
    - if it processes request concurrently their is no direct relationship between latency and throughput

- law of diminishing returns - optimizing individual components may be a waste of time

- Improving Latency
  - exploiting workload properties
    - optimize for the common case
      -have a fast path for common actions
    - a cache
    - average latency - Freq_fast x Latency_fast + Freq_slow x Latency_slow
  - concurrency
    - split the processing a stage must do into small parts

- Improving Throughput
  - Concurrency
    - hide the latency of a single request by overlapping it with other requests
    - interleaving
      - make n instances of the bottleneck stage and run them all concurrently

- Queuing and Overload
  - **service time** = the time it takes to process a request
    - average queuing delay = 1/(1 -p)
      - p = the service utilization
      - assumes requests arrive according to a random, memoryless process and have independent exponentially distributed service times
  - **offered load** = the rate of arrival of request for a service
    - **overloaded** = when the offered load is > than the capacity of the service

- Fighting Bottlenecks
  - **Batching**
    - performing several request as a group to avoid the setup overhead
    - works well when processing a request has
      - fixed delay (f)
      - variable delay (v)
      - without batching
        - processing n requests takes n x (f + v)
      - with batching
        - takes f + n x v
      - could also reorder requests
  - **Dallying**
    - delaying a request on the chance that the operation won't be needed / create more batching opportunities
  - **Speculation**
    - performing an operation in advance of receiving a request on the chance that it will be requested
    - can perform ops using otherwise idle resources

## 6.2 Multilevel Memories
- Memory Characterization
  - Capacity
  - Average random latency
  - cost = currency per storage unit
  - cell size = the # of bytes moved by a single READ or WRITE
  - Throughput
- Multilevel Memory
  - Virtual Memory Manager


# Network


## 7.1 Interesting properties of networks
- Physical Properties
	- The speed of light is finite
		- propagation delay
	- Communication environments are hostile
	- communication media have limited bandwidth
- Mechanics of sharing
	- any-to-any connection
	- sharing of communication costs
- wide range of input parameters

### 7.1.1 Multiplexing

- a link is multiplexed if it can be used for several different communications at the same time
- **isochronoues** communication
	- "equally timed" time-division multiplexing
	- requires the sending and receiving switch to follow a predefined protocol
	- frames are sent at a predefined interval and have a set size
	- hard-edged
	  - links have a set capacity
	  
- **asynchronous**
	- variable-length frame and guidance information = packet
	- connectionless transmission - switches don't need to maintain state
	- most links place a limit on the max size of a frame
		- so large packets must be split into segments and reassembled
		- they can be received out of order
	- packet forwarding network
		- packet switches routes packets to their destination
	- transit time components
		1. Propagation delay
		2. Transmission Delay
		  - depends on the size of the packet
		3. Processing delay
		  - Time required to route and validate a packet
		4. Queuing Delay
		
## 7.5 The End-to-End Layer

		
	
	





