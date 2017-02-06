# Instantiation

Instantiating a `graphology` Graph object is merely an issue of requiring an implementation and calling it with, optionally, some data & options.

```js
import Graph from 'graphology';

// Here you go:
const graph = new Graph();

// With some pre-existing data:
const graph = new Graph(data);

// With options:
const graph = new Graph(null, options);

// With both:
const graph = new Graph(data, options);
```

## Arguments

* **data** <span class="code">[Graph|SerializedGraph]</span>: pre-existing data to give to the constructor. This data can either be an existing `Graph` instance, and in this case both nodes & edges will be imported from the given graph, or a serialized graph whose format is described [here](serialization.md#format).
* **options** <span class="code">[object]</span>: options to customize the behavior of the graph & performance hints:
  * **allowSelfLoops** <span class="code">[boolean]</span> <span class="default">true</span>: should the graph allow self-loops?
  * **defaultEdgeAttributes** <span class="code">[object]</span>: default edge attributes merged with the provided ones.
  * **defaultNodeAttributes** <span class="code">[object]</span>: default node attributes merged with the provided ones.
  * **edgeKeyGenerator** <span class="code">[function]</span>: Function used internally by the graph to produce keys for key-less edges. By default, the graph will produce keys as UUID v4. For more information concerning the function you can provide, see [this](#edge-key-generator-function).
  * **indices** <span class="code">[object]</span>: Options regarding index computation. For more information, see [this](./advanced.md#indices).
  * **multi** <span class="code">[boolean]</span> <span class="default">false</span>: Should the graph allow parallel edges?
  * **type** <span class="code">[string]</span> <span class="default">"mixed"</span>: Type of the graph. One of `directed`, `undirected` or `mixed`.

## Typed constructors

Rather than providing tedious options to the constructor, one can use one of the many handy constructors provided by the implementation to create the desired graph:

```js
import {MultiDirectedGraph} from 'graphology';

const myCustomGraph = new MultiDirectedGraph();
```

By default, the `Graph` object is a simple mixed graph, but here are the different naming "components" that you can use to instantiate a more complex graph:

* **Type of the graph?**: `Directed`, `Undirected` or none (mixed graph).
* **Graph with parallel edges?**: `Multi` or none (simple graph).

Then to build the name, one must order the components likewise:

```
Multi? + Type? + Graph
```

*Examples*

```js
MultiGraph
DirectedGraph
MultiUndirectedGraph
(...)
```

---

## Edge key generator function

The provided function takes a single object describing the created edge & having the following properties:

* **undirected** <span class="code">boolean</span>: whether the edge is undirected.
* **source** <span class="code">any</span>: the source of the edge.
* **target** <span class="code">any</span>: the target of the edge.
* **attributes** <span class="code">object</span>: optional attributes.

*Example - Incremental id*

```js
const generator = (function() {
  let id = 0;

  return () => id++;
})();

const graph = new Graph(null, {edgeKeyGenerator: generator});

graph.addNodesFrom(['John', 'Martha']);
graph.addEdge('John', 'Martha');

graph.getEdge('John', 'Martha');
>>> '0'
```

*Example - Id based on edge data*

```js
const generator = function({undirected, source, target, attributes}) {
  return `${source}->${target}`;
};

const graph = new Graph(null, {edgeKeyGenerator: generator});

graph.addNodesFrom(['John', 'Martha']);
graph.addEdge('John', 'Martha');

graph.getEdge('John', 'Martha');
>>> 'John->Martha'
```
