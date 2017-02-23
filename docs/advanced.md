# Advanced

## Indices

To be efficient, it is likely that most implementations will rely on internal indices.

But, since this part is likely to be implementation-related rather than enforced by the present specifications, we cannot describe more than some generic methods and a way to provide configuration if needed.

## Reference implementation

The reference `Graph` implementation only computes a `structure` index which stores neighbors & related edges in a sparse matrix.

Note that, to save some memory sometimes, this index is lazy and will only be computed when necessary (in the case of a multi graph, it might never be computed, for instance).

### Indices-related methods

#### #.computeIndex

Forces the computation of the index.

*Example*

```js
graph.computeIndex();
```

#### #.clearIndex

Release the index from memory.

*Example*

```js
graph.clearIndex();
```
