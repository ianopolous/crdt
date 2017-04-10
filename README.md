# CRDT
A description of a new conflict free replicated data type (CRDT) for a set

# Parity-Set
This is a description of what is, to my understanding, a new implementation of a CRDT for a set, and which has clearer semantics than a PN-Set. 

Each element of the set has an associated counter which starts at zero. The parity of the counter (odd or even) decides whether the element is present. Even represents an element that isn't in the set. 

## Add:
An add operation does nothing if the element is already present. If the element is absent, then it increments the counter. 

## Remove:
A remove operation does nothing if the element is not present currently. It the element is present, then it increments the counter. 

## Merge
A merge operation takes the maximum of the counters for a given element. This clearly implies it is a state based CRDT, the counter itself is sent around, not the individual increments. 

This clearly forms a CRDT. An element can be added and removed an unlimited number of times. Unlike a PN-Set, you cannot reach a situation where an add operation doesn't end in the element being present. Compared to an OR-set CRDT, the storage space required per element (whether removed or not) is much less - O(1) rather than O(add operations on that element since the last remove).

You can reference this with, Parity-Set [Preston 2017]
