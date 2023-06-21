# msimcache

A simple cache simulator written in Rust

The Cache is a 3-dimensional array
+ The x, y dimensions define the basic structure of the cache table:
  + y: the cache entries
  + x: the content of the cache entries: Valid bit (V), Dirty bit (D), TAGfirst dimension is the associativity
+ The z dimension is the associativity:
  + 1 (direct mapped), set associative (2, 4, 8, etc.)
