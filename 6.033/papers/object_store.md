#Object Store
  

## Goals
- make fetching persistant objects as fast as transient ones

## Collections
- Create a collection attr of an obj by setting a fields if type *os_Set*
- A policy can be associated with a collection and ObjectStore transparently selects the most efficeinnt data structure for the application

## Relationships
- declare using *inverse_member*
- supports 1-1, 1-many and many-many
- These references are automatically updated to always be in sync

## Queries
- nesting supported
- doesn't support full joins, does support semi-joins i.e. result of a query is a subset of the collection being queried.

## Versioning
- a user can check out a version of an object and check it back in at a later time
- no concurrency issues because a user can simply checkout an alternate version
- meging of versions is left up to the application

## Implementation
- Tag table - keeps track of type and location of every object
- applications can ipmrove performance by clustering objects that are used together.
	- the db is split into chunks called segments
	- the app can choose what segment for objects to reside

### Collections
- os_collection - automatically chooses the proper subclass
	- os_set
	- os_bag
	- os_list

### Queries
- join optimization easy
- index maitenece hard
	- require declaration of fields that may be indexible
	- if these fields changed update index