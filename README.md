# GitHub Source Implementation: Sequential vs Parallel Traversal

**Author**: Arda Akgur  
**Last Updated**: 04/07/2025 

## Overview

This document compares two versions of our GitHub data extraction implementation:
- `github.py`: Original sequential implementation
- `github_async.py`: Optimized parallel implementation

Both versions maintain identical functionality while differing in traversal performance.

## Key Differences

| Feature                | `github.py`                     | `github_async.py`               |
|------------------------|---------------------------------|----------------------------------|
| **Traversal Approach** | Sequential DFS                 | Parallel DFS (directories only)  |
| **Concurrency**        | None                           | Up to 10 concurrent directories |
| **Performance**        | Linear time for directories    | Sub-linear time for directories |
| **Code Complexity**    | Simpler                       | Added async coordination        |
| **Error Handling**     | Standard                      | Identical to original           |
| **Output Consistency** | Fully deterministic           | Deterministic per directory     |

## Implementation Details

### Original (`github.py`)
- Processes one directory at a time
- Simple recursive DFS implementation
- Easier to debug
- Better for small repositories

### Optimized (`github_async.py`)
```python
MAX_CONCURRENT_DIRECTORIES = 10  # Configurable concurrency limit

async def _traverse_directory(...):
    # Process files sequentially
    for file in files:
        ...
    
    # Process directories in parallel
    async with semaphore:
        ...
