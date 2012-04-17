# Performance

## 6.1 Performance Metrics

-  capacity - a measure of a service's size
-  utilization - the percentage of capacity of a reasource that is used
-  overhead - in a layered application its what the layers below it use
-  useful work - what is abailible to the application
  - e.g. if 10% of a disk is used for file system data structures then from the applications pov 10% is overhead of the fs and 90% is useful capacity
  
-  latency 
  - delay between a change at the input to a system and the corresponding change at its output
  - pipelining
    - latency_a+b >= latency_a + latency_b

-  throughput
  - the rate of useful work done by a service