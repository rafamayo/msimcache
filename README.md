# msimcache

A simple cache simulator written in Rust

The Cache is a 3-dimensional array
+ The x, y dimensions define the basic structure of the cache table:
  + y: the cache entries
  + x: the content of the cache entries: Valid bit (V), Dirty bit (D), TAG
+ The z dimension is the associativity:
  + 1 (direct mapped), set associative (2, 4, 8, etc.)


### Command line example
msimcache --size 64 --block 32 --assoc 2 --write 0 --evict 0 --trace example1.trace

+ --size Cache size in KiB
+ -block Block size in Byte
+ --assoc associativity:
  + 1 (direct mapped)
  + 2, 4, 8, etc. (set associative)
  + 0 (full associative)
+ --write write behaviour
  + 0 write back / write allocate
  + 1 write through / non write allocate
+ --evict eviction strategy
  + 0 RANDOM
  + 1 FIFO
  + 2 LRU
+ -trace trace file

### Creating the data structure

Computing the size of the data structure from the arguments
Assumptions:
+ The adresses are 32 bit long
+ The cache size is given in KiB
+ The block size is given in Byte
+ The associativity is given as the number of slots

We need associativity, number of sets and TAG size

Index bits: `bi = log2 s + 10 - log2 b - log2 a`

Offset bits: `bo = log2 b`

TAG bits: `bt = 32 - bi - bo`
