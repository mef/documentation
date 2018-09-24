# Iteration

Using a `Graph` instance, it is possible to iterate on the three following things:

* [Nodes](#nodes)
* [Edges](#edges)
* [Neighbors](#neighbors)

**Iteration methods**

The library basically proposes two ways to iterate:

* Methods returning arrays of keys.
* Methods creating JavaScript [iterators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators) for lazy consumption (yet to be implemented!).

**On what do we iterate?**

Note that the methods will always iterate on nodes' & edges' keys and nothing more. If you need to access to attributes during iteration, you can do so using the [attributes](attributes.md) methods.

## Nodes

Those methods iterate over the graph instance's nodes.

**Examples**

```js
const graph = new Graph();

graph.addNode('Thomas');
graph.addNode('Elizabeth');

// Using the array-returning method:
graph.nodes();
>>> ['Thomas', 'Elizabeth']
```

**Methods**

```
#.nodes
```

**Arguments**

1. **None**: iterate over every node.

## Edges

These methods iterate over the graph instance's edges.

**Examples**

```js
const graph = new Graph();

graph.addNodesFrom(['Thomas', 'Rosaline', 'Emmett', 'Catherine', 'John', 'Daniel']);
graph.addEdgeWithKey('T->R', 'Thomas', 'Rosaline');
graph.addEdgeWithKey('T->E', 'Thomas', 'Emmett');
graph.addEdgeWithKey('C->T', 'Catherine', 'Thomas');
graph.addEdgeWithKey('R->C', 'Rosaline', 'Catherine');
graph.addEdgeWithKey('J->D1', 'John', 'Daniel');
graph.addEdgeWithKey('J->D2', 'John', 'Daniel');

// Using the array-returning methods:
graph.edges();
>>> ['T->R', 'T->E', 'C->T', 'R->C']

graph.edges('Thomas');
>>> ['T->R', 'T->E', 'C->T']

graph.edges('John', 'Daniel');
>>> ['J->D1', 'J->D2']
```

**Methods**

```
#.edges
#.inEdges
#.outEdges
#.inboundEdges (in + undirected)
#.outboundEdges (out + undirected)
#.directedEdges
#.undirectedEdges
```

**Arguments**

1. **None**: iterate over every edge.
2. **Using a node's key**: will iterate over the node's relevant attached edges.
  * **node** <span class="code">any</span>: the related node's key.
3. **Using source & target**: will iterate over the relevant edges going from source to target.
  * **source** <span class="code">any</span>: the source node's key.
  * **target** <span class="code">any</span>: the target node's key.

## Neighbors

These methods iterate over the neighbors of the given node or nodes.

**Examples**

```js
const graph = new Graph();

graph.addNodesFrom(['Thomas', 'Rosaline', 'Emmett', 'Catherine', 'John', 'Daniel']);
graph.addEdge('Thomas', 'Rosaline');
graph.addEdge('Thomas', 'Emmett');
graph.addEdge('Catherine', 'Thomas');
graph.addEdge('Rosaline', 'Catherine');
graph.addEdge('John', 'Daniel');
graph.addEdge('John', 'Daniel');

// Asking whether two nodes are neighbors:
graph.neighbors('Thomas', 'Rosaline');
>>> true

// Using the array-returning methods:
graph.neighbors('Thomas');
>>> ['Rosaline', 'Emmett', 'Catherine']
```

**Methods**

```
#.neighbors
#.inNeighbors
#.outNeighbors
#.inboundNeighbors (in + undirected)
#.outboundNeighbors (out + undirected)
#.directedNeighbors
#.undirectedNeighbors
```

**Arguments**

1. **Using a node's key**: will iterate over the node's relevant neighbors.
  * **node** <span class="code">any</span>: the node's key.
2. **Using two nodes' keys**: will return whether the two given nodes are neighbors.
  * **node1** <span class="code">any</span>: first node.
  * **node2** <span class="code">any</span>: second node.
