# Lecture 11
### Network Layer
1. Forwarding
	- send data over links according to a routing table
2. Routing
	- process through which routing tables are build
	- Path Vector Algorithm
	- Each node keeps a forwarding table T
		- Destination
		- Link
		- Path
	- two steps
		- advertise - periodically send T to neighbors
		- integrate(N, neighbor, link) 
			- on receipt of advertisement from neighbor merge table N received on link into T
		 	- merge(N, link, T)
		 	```python
		 	for each dest d w/path r in N:
		 		if d not in T:
		 			add (d, link, neighbor ++ r) to T
		 		if d is in T:
		 			replace if (neighbor ++ r) is shorter than old path
		 	```
	