# Bipartite Matching Algorithm
Extension of a **Ford Fulkerson** max flow problem using **depth first search**

## Problem Statement
Given an undirected bipartite graph, find the maximum matching between left & right halves. Each node in the **Left half `L`** mapped to at most 1 node in `R`. Similarly, each node in the **Right Half `R`** is mapped to at most 1 node in `L`  
**Goal:** maximize the number of matchings

## Algorithm
Convert to a Max Flow / Min Cut problem by making a **directed graph**:
1. Make all edges from `L` to `R` directed with capacity `1`  
A flow of `1` corresponds to *yes there's a matching* and `0` mean *no matching*  
Since there's only 2 values, it could even be implemented as a `boolean`
2. Add a **Source `S`** & create directed edges from `S` to every vertex in the left half with capacity `1`
3. Add a **Sink `T`** & create directed edges from every vertex in the right half to `T` with capacity `1`
4. Use Ford-Fulkerson algorithm to find the max flow
  
## Usage (setting things up in `main()`)
- Graph is represented as an **edge list**
- `vertexCount` must be an accurate number of nodes in the graph
- `getStringVertexIdFromArrayIndex` allows conversion between the array indexes used by the actual algorithm & the human-readable names of the vertices. These are sequential with `"S"` and `"T"` being added at the end
- `S` & `T` are added to the end of the list of vertices with **`S` getting array index `vertexCount`** and **`T` getting array index `vertexCount+1`**
- `int[] leftHalfVertices` contains the array indexes of the vertices in the left part of the bipartite graph
- Similarly, `int[] rightHalfVertices` contains the vertices in the right half
- **These must be *consecutive integers* with the 1st number in `rightHalfVertices` being 1 greater than the last number in `leftHalfVertices`**
- Use `addEdge()` method on `BipartiteMatching` class to add new edges  
The initial bipartie graph is undirected so **undirected edges should only be added once**. They are converted to directed edges when finding the max flow
- Run `connectSourceToLeftHalf()` to modify the graph & add the source, then `connectSinkToRightHalf()` to connect the sink
- Run `fordFulkersonMaxFlow(source, sink)` to find the maximum matching

### Starting Graphs
<img src='images/graph1.png' width='400'>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <img src='images/graph2.png' width='400' >

### Relabeled Graphs
The code uses array indexes instead of nice human-readable Vertex names. Red numbers represent **array indexes**
<img src='images/graph1-renamed-array-indexes.png' width='400'>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <img src='images/graph2-renamed-array-indexes.png' width='400' >

### Directed Graphs With Source & Sink Added
*All edge capacities are `1` but omitted here for clarity of the picture*  
<img src='images/graph1-flow-network.png' width='400'>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <img src='images/graph2-flow-network.png' width='400' >

### Maximum Matching Solutions
These are not unique, but these are what the program finds  
<img src='images/graph1-max-matching.png' width='400'>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <img src='images/graph2-max-matching.png' width='400' >
