# Iteration

Using a `Graph` instance, it is possible to iterate on the three following things:

* [Nodes](#nodes)
* [Edges](#edges)
* [Neighbors](#neighbors)

**Iteration methods**

The library basically proposes three ways to iterate:

* Methods returning arrays of keys.
* Methods using callbacks.
* Methods creating JavaScript [iterators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators) for lazy consumption (yet to be implemented!).

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

// Using the callback method
graph.forEachNode((node, attributes) => {
  console.log(node, attributes);
});
```

<h3 id="nodes-array">#.nodes</h3>

Returns an array of node keys.

### #.forEachNode

Iterates over each node using a callback.

**Arguments**

* **callback** <span class="code">function</span>: callback to use.

**Callback arguments**

* **key** <span class="code">string</span>: the node's key.
* **attributes** <span class="code">object</span>: the node's attributes.

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

// Using the callback methods
graph.forEachEdge(
  (edge, attributes, source, target, sourceAttributes, targetAttrubutes) => {
    console.log(`Edge from ${source} to ${target}`);
});

// And the counterparts
graph.forEachEdge('Thomas', callback);
graph.forEachEdge('John', 'Daniel', callback);
```

<h3 id="edges-array">#.edges</h3>

Returns an array of relevant edge keys.

**Counterparts**

```
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

### #.forEachEdge

Iterates over relevant edges using a callback.

**Counterparts**

```
#.forEachInEdge
#.forEachOutEdge
#.forEachInboundEdge (in + undirected)
#.forEachOutboundEdge (out + undirected)
#.forEachDirectedEdge
#.forEachUndirectedEdge
```

**Arguments**

1. **Callback**: iterate over every edge.
  * **callback** <span class="code">function</span>: callback to use.
2. **Using a node's key**: will iterate over the node's relevant attached edges.
  * **node** <span class="code">any</span>: the related node's key.
  * **callback** <span class="code">function</span>: callback to use.
3. **Using source & target**: will iterate over the relevant edges going from source to target.
  * **source** <span class="code">any</span>: the source node's key.
  * **target** <span class="code">any</span>: the target node's key.
  * **callback** <span class="code">function</span>: callback to use.

**Callback arguments**

* **key** <span class="code">string</span>: the edge's key.
* **attributes** <span class="code">object</span>: the edge's attributes.
* **source** <span class="code">string</span>: key of the edge's source.
* **target** <span class="code">string</span>: key of the edge's target.
* **sourceAttributes** <span class="code">object</span>: attributes of the edge's source.
* **targetAttributes** <span class="code">object</span>= attributes of the edge's target.

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

// Using the callback methods:
graph.forEachNeighbor('Thomas', function(neighbor, attributes) {
  console.log(neighbor, attributes);
});
```

<h3 id="neighbors-array">#.neighbors</h3>

Returns an array of relevant neighbor keys.

**Counterparts**

```
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

### #.forEachNeighbor

Iterates over the relevant neighbors using a callback.

**Counterparts**

```
#.forEachInNeighbor
#.forEachOutNeighbor
#.forEachInboundNeighbor (in + undirected)
#.forEachOutboundNeighbor (out + undirected)
#.forEachDirectedNeighbor
#.forEachUndirectedNeighbor
```

**Arguments**

* **node** <span class="code">any</span>: the node's key.
* **callback** <span class="code">function</span>: callback to use.

**Callback arguments**

* **key** <span class="code">string</span>: the neighbor's key.
* **attributes** <span class="code">object</span>: the neighbor's attributes.

