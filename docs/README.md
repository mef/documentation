# Graphology

`graphology` is a specification and reference implementation for a robust & multipurpose JavaScript `Graph` object.

It aims at supporting various kinds of graphs with the same unified interface.

A `graphology` graph can therefore be directed, undirected or mixed and can be simple or support parallel edges.

Along with those specifications, one will also find a [standard library](#standard-library) full of graph theory algorithms and common utilities such as graph generators, layouts etc.

## Installation

To install the reference implementation:

```bash
npm install --save graphology
```

The source of the reference implementation can be found on [this](https://github.com/graphology/graphology) github repository.

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

## Standard library

* [graphology-assertions](https://github.com/graphology/graphology-assertions#readme)<br>*Miscellaneous assertions (same nodes, same edges etc.).*
* [graphology-centrality](https://github.com/graphology/graphology-centrality#readme)<br>*Various centrality measures (degree, betweenness etc.).*
* [graphology-components](https://github.com/graphology/graphology-components#readme)<br>*Connected components (strong, weak etc.).*
* [graphology-generators](https://github.com/graphology/graphology-generators#readme)<br>*Graph generators (random graphs, complete graphs etc.).*
* [graphology-gexf](https://github.com/graphology/graphology-gexf#readme)<br>*Parsers & writers for the GEXF file format.*
* [graphology-hits](https://github.com/graphology/graphology-hits#readme)<br>*HITS algorithm.*
* [graphology-layout](https://github.com/graphology/graphology-layout#readme)<br>*Basic graph layouts (random, circle etc.).*
* [graphology-operators](https://github.com/graphology/graphology-operators#readme)<br>*Graph unary & binary operators (reverse, union, intersection etc.)*
* [graphology-shortest-path](https://github.com/graphology/graphology-shortest-path#readme)<br>*Shortest path functions (Dijkstra, A&ast; etc.)*
* [graphology-utils](https://github.com/graphology/graphology-utils#readme)<br>*Miscellaneous utils used by most of the other modules.*

## Implementing graphology

`graphology` merely is a specification so that anyone can implement it its own way if necessary while keeping the advantages of being able to use the [standard library](#standard-library).

Graphs are complex structures and, while we designed the reference implementation to handle most common cases with good performance, one will always be able to implement the present specifications in a more performant fashion for very specific use cases.

It is therefore possible to test your custom implementation against the specifications' unit tests.

Directions about this can be found [here](unittests.md).
