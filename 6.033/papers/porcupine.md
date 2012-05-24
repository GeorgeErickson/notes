# Porcupine
A small scalable mail server

## Design
### Goals
1. Manageability
	- **self-configure**
	- **self-heal**
2. Availiblity
	- avoid failure where whole groups of users lose mail service
3. Performance
	- scale lineraly with number of nodes in the system

### Implementation
1. **functional homogeneous**
	- any node can execute all or part of a transaction
2. **dynamically scheduled**
	- every tansaction is dynamically scheduled
	- ensures uniform load across nodes
3. **automatically reconfigures**
	- recongiures tranparently when nodes are added or removed
4. **replication**
	- system/user data are replicated across a number of nodes to ensure availiblity

## Architecture
1. Replicated State
	- hard state = info that can't be lost
	- soft state - info that can be reconstructed using a full disk scan
2. Data structures
	1. Mailbox fragment = collection of messages stored for a given user on a given node (hard)
	2. Mailbox fragment list = list of the nodes containing the mailbox fragments for a user (soft)
	3. user profile db = (hard)
	4. user profile soft state = each entry in the user profile db is kept as soft state on exactly one node (soft)
	5. user map = table that maps user to the node with their user profile soft state (soft and replicated on each node)
	6. Cluster membership list = each node maintains a list of nodes that are part of the cluster (soft and replicated on each node)
3. Data stucture managers
	- user manager
		- manages soft state of users
		- allows larger user populations to be sorted 
		- maintains mailbox fragment list
	- membership manager
	- mailbox manager
	- user profile manager
	- replication manager