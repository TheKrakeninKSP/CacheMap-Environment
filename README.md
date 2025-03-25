# Cache Map Environment

## Overview
This project explores the performance differences between a **single-level cache** and a **multi-level cache system with additional buffers** (victim cache, write buffer, and prefetch buffers). It simulates memory access patterns and evaluates how different cache configurations impact cache hit rates and overall performance.

## Features
- **Simulated Memory Hierarchy:** Implements different levels of cache memory and buffers.
- **Cache Policies:** Fully associative, direct-mapped, and k-way set-associative cache configurations.
- **Buffers:** Victim cache, write buffer, and prefetch buffers.
- **CPU Simulation:** Simulates CPU memory accesses, writes, and prefetching.
- **Performance Metrics:** Measures cache hit rates, global miss rate, spatial locality, and temporal locality.

## Code Structure
### Memory and Cache Classes
- **Word:** Represents a single 64-bit memory word.
- **Frame:** Represents a block of memory containing multiple words.
- **MemFrame:** Frame in main memory.
- **CacheFrame:** Frame in the cache with metadata (valid, clean, tag, LRU time).

### Memory Hierarchy
- **Memory (Base Class):** Defines size, speed, and access tracking.
- **Mainmem:** Represents main memory (RAM).
- **Cachemem:** Represents cache memory, supporting different mapping strategies:
  - **FullyAssociativeCache**
  - **DirectMappedCache**
  - **KWaySetAssociativeCache**

### Buffers
- **Victim Cache:** Stores evicted blocks to reduce miss penalty.
- **Write Buffer:** Holds data before writing back to main memory.
- **Prefetch Buffers:** Anticipates future memory accesses.

### CPU Simulation
- **Access Handling:** Reads from/write to memory through cache hierarchy.
- **Prefetching:** Fetches likely-to-be-used data in advance.

### Helper Functions
- **Locality Analysis:** Measures spatial and temporal locality.
- **Sequence Generator:** Generates memory access patterns.
- **Hierarchy Analysis:** Simulates memory accesses and records performance.

## Some sample experiments & results
### Experiment 1: Single-Level Cache
#### Configuration:
- Main Memory: 64K words (4096 blocks)
- Fully Associative Cache: 2K words (128 blocks)
- CPU accesses through the cache

#### Results:
- **Cache Hit Rate:** 90.48%
- **Global Miss Rate:** 9.52%
- **Locality Scores:** Spatial - 0.854, Temporal - 0.869
- **Observation:** Higher miss rate due to limited capacity and lack of buffers.

### Experiment 2: Multi-Level Cache with Buffers
#### Configuration:
- **L1 Cache:** Direct-mapped (2K words, 128 blocks)
- **L2 Cache:** 4-way set-associative (16K words, 1024 blocks)
- **Buffers:** Victim (4 blocks), Write (4 blocks), Prefetch (4 blocks each for data & instructions)

#### Results:
- **L1 Cache Hit Rate:** 81.16%
- **L2 Cache Hit Rate:** 94.14%
- **Global Miss Rate:** 1.10%
- **Observation:** Buffers and L2 cache significantly reduce misses.

## Key Takeaways
- **Multi-level caches improve performance** by reducing accesses to main memory.
- **Buffers further optimize performance** by reducing penalties from cache misses.
- **Spatial and temporal locality significantly impact cache efficiency.**

