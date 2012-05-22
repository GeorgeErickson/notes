# Unison
## Design
- users changes are sacred
- user level program, syncs using the current state of the system
	- not trace-based sync
- portable across large number of OS
- high performance syncing large (1GB) replicas
- users should be able to predict is behavior in all situations
- Only syncs whole files, conflict if the same file has been edited in two versions
- Only supports pairwise sync

## Architecture
- client process started with 2 roots for sync
- *update detection* performed separately by the client and server
	- read a archive file created at the end of the last sync
	- compare this with current state to figure out a list of paths that have changed
		- a file is changed if it contents are different
- *reconciliation* lists are merged to create a *task list*
	- deletion is considered as a special kind of content, so it is treated the same as created and changed files
	- conflicts - a path is in conflict if
		1. it has been updated in one replica
		2. it or any of its descendents have been updated in the other replica
		3. its contents in the in the two replicas are not identical
		- this means that deleting a directory in one replica and changing a descendent of that directory in the other is a conflict
- *confirmation* - task list displayed to user
- *propogation* propogate the changes between replicas

## Robustness
### Crash resistance
- At every moment during a run of unison, every file has either its original contents or its correct final contents
- atomic file replacement
	- the file to be replaced is renamed to a temp file
	- the replacement file is renamed to the target file
- this atomic file replacment required in two places
	1. updating a user file
		- transfers new version over network to make temp file (not atomic)
	2. updating its archive
		- could be interuptd after its updated user file but before archive updated
			- this is ok

### concurrent file sytem updates
1. user may modify file after unison decides it should be replaced
	- unison checks for this by refingerprinting a file immedietly before it writes over it
2. user modifies file while unison is in the middle of transfering it

### Update Detection
- if a file is changed and unison does not detect this, data may be lost
- modtimes
	- not sufficient because they dont change when a file is renamed
	- if A and B have same modtime and A is deleted and B is renamed to A, modtimes would show no change to A
	- on Unix this can be detected with inodes, but not 100% because modtimes can be set back
- only sure way is to compare the fingerprint of every file
	- takes a long time
	- for impatient users less-safe method included
	
### Transfer Errors
- checksums

### Archive loss
- user deletes archive file
- behaves as though both replicas had been completely empty at the last sync

### Error handling
- Safe for the program to crash at anytime

### Cross-platform sync
1. Case sensitivity of file names
	- treat both files sytems as case insensitive
	- if finds two files with diff capitalization, displays warning that it cant be synced to windows 
2. File permissions
	- UNIX
		- file has an owner and a group
		- can specify read/write/execute permissions sperately for all
	- Windows
		- no owners or group
		- only read-only/write-only

		
3. Symbolic Links
4. Illegal file names
5. modtime granularity
6. Reconciling line endings
7. mounted disks

## Performance
1. Threads
2. Rsync