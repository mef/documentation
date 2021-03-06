## Example: Reversing a graph

```js
/**
 * Function taking a graph & creating its reverse by reversing its
 * directed edges.
 */
export function reverse(graph) {
  const reversed = graph.emptyCopy();

  // Importing the nodes:
  reversed.importNodes(graph.exportNodes());

  // Importing undirected edges:
  reversed.importEdges(graph.exportUndirectedEdges());

  // Reversing directed edges:
  graph.directedEdges().forEach(edge => {
    const [source, target] = graph.extremities(edge);

    reversed.addDirectedEdgeWithKey(
      edge,
      target,
      source,
      graph.getAttributes(edge)
    );
  });
}
```
