# Performance

## 6.1 Performance Metrics

-  capacity - a measure of a service's size
-  utilization - the percentage of capacity of a reasource that is used
-  overhead - in a layered application its what the layers below it use
-  useful work - what is abailible to the application
  - e.g. if 10% of a disk is used for file system data structures then from the applications pov 10% is overhead of the fs and 90% is useful capacity
  
-  latency 
  - low is good
  - delay between a change at the input to a system and the corresponding change at its output
  - pipelining - latency_a+b >= latency_a + latency_b

-  throughput
  - the rate of useful work done by a service
  - throughput_a+b <= minumum(throughput_a, throughput_b)
  - when a stage processes request serially the throughput and the latency are directly related
    - throughput = 1 / latency
    - if it processes request concurently their is no direct relationship between latency and throughput

- law of diminishing returns - optimizing individual components may be a waste of time

- Improving Latency
  - exploiting workload properties
    - optimize for the common case
      -have a fast path for common actions
    - a cache
    - average latency - Freq_fast x Latency_fast + Freq_slow x Latency_slow
  - concurency
    - split the processing a stage must do into small parts

- Improving Throughput
  - Concurrency
    - hide the latency of a single request by overlapping it with other requests
    - interleaving
      - make n instances of the bottleneck stage and run them all concurrently

- Queuing and Overload
  - service time = the time it takes to process a request
    - average queuing delay = 1/(1 -p)
      - p = the service utilization
      - assumes requests arrive according to a random, memoryless process and have independant exponentially distributted service times
  - offered load = the rate of arrival of request for a service








