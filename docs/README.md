# Graphology

`graphology` is a specification and reference implementation for a robust & multipurpose JavaScript `Graph` object.

It aims at supporting various kinds of graphs under a same unified interface.

A `graphology` graph can therefore be directed, undirected or mixed and can be simple or support parallel edges.

Along with those specifications, one will also find a [standard library](standard-library.md) full of graph theory algorithms and common utilities such as graph generators etc.

## Installation

To install the reference implementation:

```bash
npm install --save graphology
```

## Quick Start

```js
const Graph = require('graphology');

const graph = new Graph();
graph.addNode('John');
graph.addNode('Martha');
graph.addEdge('John', 'Martha');

console.log('Number of nodes', graph.order);
console.log('Number of edges', graph.size);

console.log('Nodes', graph.nodes());
```

## Implementing graphology

`graphology` merely is a specification so that anyone can implement it its own way if necessary while keeping the advantages of being able to use the [standard library](standard-library.md).

Graphs are complex structures and, while we designed the reference implementation to handle most common cases with good performance, one will always be able to implement the present specifications in a more performant fashion for very specific use cases.

It is therefore possible to test your custom implementation against the specifications' unit tests.

Directions about this can be found [here](unittests.md).
