# Graphology

`graphology` is a specification for a robust & multipurpose JavaScript `Graph` object and aiming at supporting various kinds of graphs under a same unified interface.

`graphology` therefore handles directed, undirected & mixed graphs which can be either simple or have parallel edges.

Along with those specifications, one will also find a standard library full of graph theory algorithms and common utilities.

So, even if we propose a reference implementation, anyone remains free to implement the present specifications and still be able to use the standard library & all the relevant libraries coded to work with `graphology`.

## Installation

To install the reference implementation:

```bash
npm install --save graphology
```

## Quick Start

```js
import Graph from 'graphology';

// Let's create our graph:
const graph = new Graph();

// Let's add some nodes representing people:
graph.addNode('Jack', {age: 56});
graph.addNode('John', {age: 13});
graph.addNode('Catherine', {age: 15});
graph.addNode('Martha', {age: 94});

// And some relations between them:
graph.addEdge('Jack', 'John', {type: 'FATHER_OF'});
graph.addEdge('Jack', 'Catherine', {type: 'FATHER_OF'});
graph.addEdge('Martha', 'Jack', {type: 'MOTHER_OF'});

// How many nodes do we have?
console.log(graph.order);
>>> 4

// And how many edges?
console.log(graph.size);
>>> 5

// Let's print the age of every person:
graph.nodes().forEach(function(node) {
  console.log(graph.getNodeAttribute(node, 'age'));
});

// Let's find the children of Jack:
const edges = graph.outEdges('Jack');

const children = edges
  .filter(edge => graph.getEdgeAttribute(edge, 'type') === 'FATHER_OF')
  .map(edge => graph.relatedNode('Jack', edge));

console.log(children);
>>> ['John', 'Catherine']
```
