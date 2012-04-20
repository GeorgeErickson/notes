# Lecture 11 - Network Layer
1. Forwarding
	- send data over links according to a routing table
	- get a packet
		1. lookup packets dest in forwarding table
			- if found, send to correct link
			- else, drop packet
		2. decrement TTL and drop packet if 0
			- TTL used to discard lost packets
		3. checksum
		4. forward packet to outgoing port
		5.  transmit packet onto link
2. Routing
	- process through which routing tables are build
	- Path Vector Algorithm
		- Algorithm
			1. Initialize
				- Each node keeps a forwarding table T
					- Destination
					- Link
					- Path
				- each node knows path to itself
			2. *advertise* - periodically send T to neighbors
				- at the end of the first round every node has learned all one-hop paths
			3. *integrate*(N, neighbor, link) 
				- on receipt of advertisement from neighbor merge table N received on link into T
			 	- merge(N, link, T)
			 	<pre>
			 	for each dest d w/path r in N:
			 		if d not in T:
			 			add (d, link, neighbor ++ r) to T
			 		if d is in T:
			 			replace if (neighbor ++ r) is shorter than old path
			 	</pre>
	 	- Questions
	 		- How do we avoid Permanent Loops?
	 			- don't pick paths with ourselves in them (this is why the *path* is necessary)
	 		- What happens when the graph changes?
	 			- Deals well with the addition of new links
	 			- To deal with links that go down, each router should discard any path that a neighbor stop advertising

# Lecture 12 - Peer-to-Peer systems
1. Parts
	- Publisher
		- a torrent file
			- url of tracker
			- file name, length
			- SHA1s of data blocks
	- Tracker
		- organizes a swarm of peers (who has what block)
	- Seed
		- posts the URL for torrent with tracker
		- has a complete copy of the file
		- every peer that is online that has a copy of a file becomes a seed
	- Peer asks tracker for a list of peers to download from
		- tracker returns list with random selection of peer
	- Peers contact other peers to see what parts can be downloaded
2. Transport
	- Peers pipeline on top of TCP
3. Which pieces to download
	- random for first piece, then rarest first, parallel for last piece
4. Removing central component of BitTorrent the **Tracker** - use a DHT
	- Distributed Hash Table - Chord
		- log n messages per lookup
		- log n state per node
		- survives massive failures
		- node keys are arranged in a circle that can have at most 2^m nodes
	- Chord ID's
		- key identifier = SHA1 (key)
		- node identifier = SHA1 (IP address)
		- both are uniformly distributed in the same ID space
	- Mapping key id's to node ids
		- key stored on fi
		- each node n keeps a finger table containing up to m entries
		- finger[i] = successor # (n+2^(i-1))
		
# Lecture 13 - TCP
- Semantics
	- 3 packet handshake to set up connection
	- does not guarantee at most once delivery
	- ignoring slow start
		- window <= min(buffer, bottleneck_cap * RTT)
	- congestion control
		- increase congestion window (*cwnd*) slowly, window <= min(receiver_buffer, cwnd)
		- basic idea
			- increase cwnd slowly; if no drops no congestion yet
			- if a drop occurs, decrease cwnd quickly
		- additive increase multiplicative decrease (AIMD)
			- every RTT (Round Trip Time)
				- no drop: cwnd = cwnd + 1
				- a drop cwnd = cwnd / 2
			- leads to efficiency and fairness
			- transmission rate = W/RTT
			
# Lecture 14 - Fault-tolerant computing
# Lecture 15 - Atomicity
### All or nothing atomicity
1. Shadow Copy
	- write to copy of data, atomically switch to new copy
	- switching can be done tim one all-or-nothing operation (sector-write)
	- only make one write to current/live copy of data
	- problems
		- only works on a single disk
		- one operation at a time
# Lecture 16 - Logging
- Idea - keep a log of all changes, and whether each change commits or aborts
				
			