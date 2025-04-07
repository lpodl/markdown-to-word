# Traveling Salesman Problem (TSP)

## Problem Description

The Traveling Salesman Problem (TSP) is a classic optimization problem where a salesman must visit a set of cities exactly once and return to the starting city, while minimizing the total distance traveled.

## Binary Model

The TSP can be formulated as finding a minimum-cost Hamiltonian cycle in a complete graph, where:
- Nodes represent cities
- Edges represent paths between cities with associated distances

### Parameters

- $N$ = Number of cities
- $d_{ij}$ = Distance between cities $i$ and $j$

### Decision Variables

We use binary variables $x_{i,j,p}$ where:
- $i, j \in \{1, 2, ..., N\}$ represent cities
- $p \in \{1, 2, ..., N\}$ represents position in the tour
- $x_{i,j,p} = 1$ if the salesman travels from city $i$ to city $j$ at position $p$ in the tour, and 0 otherwise

### Objective Function

The objective is to minimize the total distance traveled

$$\min \sum_{i=1}^N \sum_{j=1}^N \sum_{p=1}^N d_{ij} \cdot x_{i,j,p}$$

### Constraints

#### 1. Each city must be departed from exactly once

$$\sum_{j=1}^N \sum_{p=1}^N x_{i,j,p} = 1 \quad \forall i \in \{1,2,...,N\}$$

...


## Code

 We don't have to bother with a binary implementation, we can use NL solver!

```python
from dwave.optimization.generators import traveling_salesperson
from dwave.system import LeapHybridNLSampler
DISTANCE_MATRIX = [
    [0, 656, 227, 578, 489],
    [656, 0, 889, 141, 170],
    [227, 889, 0, 773, 705],
    [578, 141, 773, 0, 161],
    [489, 170, 705, 161, 0]]
model = traveling_salesperson(distance_matrix=DISTANCE_MATRIX)
sampler = LeapHybridNLSampler()     
results = sampler.sample(
    model,
    label='SDK Examples - TSP')     
```
