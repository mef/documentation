# Attributes

## Nodes

### #.getNodeAttribute

Returns the desired node's attribute.

*Example*

```js
graph.addNode('Martha', {age: 34});

const age = graph.getNodeAttribute('Martha', 'age');

console.log(age);
>>> 34
```

*Arguments*

* **node** <span class="code">any</span>: the target node.
* **attribute** <span class="code">string</span>: name of the attribute to retrieve.

### #.getNodeAttributes

Returns the desired node's attributes or `undefined` if not found.

*Example*

```js
graph.addNode('Martha', {age: 34, eyes: 'blue'});

graph.getNodeAttributes('Martha');
>>> {
  age: 34,
  eyes: 'blue'
}
```

### #.hasNodeAttribute

Returns whether the desired node's attribute is set.

*Example*

```js
graph.addNode('Martha', {eyes: 'blue'});

graph.hasNodeAttribute('Martha', 'eyes');
>>> true

graph.hasNodeAttribute('Martha', 'age');
>>> false
```

### #.setNodeAttribute

Set the attribute of a node to the given value.

*Example*

```js
graph.addNode('Martha', {age: 36, eyes: 'blue'});

graph.setNodeAttribute('Martha', 'age', 34);
```

*Arguments*

* **node** <span class="code">any</span>: the node to update.
* **attribute** <span class="code">string</span>: name of the attribute to set.
* **value** <span class="code">any</span>: value to set.

### #.updateNodeAttribute

Update the attribute of a node using the provided function.

This method is very useful when performing tasks such as incrementing an attribute so you don't have to first fetch the former value to compute the next one.

Note that if the attribute is not yet setted, the passed value will be `undefined`.

*Example*

```js
graph.addNode('Martha', {occurrences: 1});

graph.updateNodeAttribute('Martha', 'occurrences', n => n + 1);
```

*Arguments*

* **node** <span class="code">any</span>: the node to update.
* **attribute** <span class="code">string</span>: name of the attribute to update.
* **updater** <span class="code">function</span>: function used to perform the update.

### #.removeNodeAttribute

Remove the given node's attribute altogether.

*Example*

```js
graph.addNode('Martha', {age: 34});

graph.removeNodeAttribute('Martha', 'age');

graph.hasNodeAttribute('Martha', 'age');
>>> false
```

### #.replaceNodeAttributes

Completely replace one node's attributes by the provided object.

*Example*

```js
graph.addNode('Martha', {age: 36, eyes: 'blue'});

graph.replaceNodeAttributes('Martha', {
  age: 34,
  eyes: 'green'
});
```

*Arguments*

* **node** <span class="code">any</span>: the node to update.
* **attributes** <span class="code">object</span>: the new attributes.


### #.mergeNodeAttributes

Merge the current attributes of a node with the provided object.

*Example*

```js
graph.addNode('Martha', {age: 36, eyes: 'blue'});

graph.mergeNodeAttributes('Martha', {age: 34, hair: 'brown'});
```

*Arguments*

* **node** <span class="code">any</span>: the node to update.
* **data** <span class="code">object</span>: data to merge.

**Performance tip**: while this method is convenient, you'll be faster by using the [`#.setNodeAttribute`](#setnodeattribute) method etc. in most cases and you'll enable renderers reacting to the graph's changes to act more efficiently, for instance.

## Edges

### #.getEdgeAttribute

Returns the desired edge's attribute or `undefined` if not found.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Catherine');
const edge = graph.addEdge('Martha', 'Catherine', {type: 'KNOWS'});

// Using the edge's key:
graph.getEdgeAttribute(edge, 'type');
>>> 'KNOWS'

// Using the edge's source & target:
graph.getEdgeAttribute('Martha', 'Catherine', 'type');
>>> 'KNOWS'
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the target edge.
  * **attribute** <span class="code">string</span>: name of the attribute to retrieve.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attribute** <span class="code">string</span>: name of the attribute to retrieve.

### #.getEdgeAttributes

Returns the desired edge's attributes.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Catherine');
const edge = graph.addEdge('Martha', 'Catherine', {type: 'KNOWS', weight: 2});

// Using the edge's key:
const attributes = graph.getEdgeAttributes(edge);

// Using the edge's source & target:
graph.getEdgeAttributes('Martha', 'Catherine');
>>> {
  type: 'KNOWS',
  weight: 2
}
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the target edge.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.

### #.hasEdgeAttribute

Returns whether the desired edge's attribute is set.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Catherine');
const edge = graph.addEdge('Martha', 'Catherine', {type: 'KNOWS'});

// Using the edge's key:
const type = graph.hasEdgeAttribute(edge, 'type');
>>> true

// Using the edge's source & target:
graph.hasEdgeAttribute('Martha', 'Catherine', 'type');
>>> 'KNOWS'
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the target edge.
  * **attribute** <span class="code">string</span>: name of the attribute to poll.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attribute** <span class="code">string</span>: name of the attribute to poll.

### #.setEdgeAttribute

Set the attribute of an edge to the given value.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Jack');
const edge = graph.addEdge('Martha', 'Jack', {type: 'KNOWS'});

// Using the edge's key:
graph.setEdgeAttribute(edge, 'type', 'LIKES');

// Using the edge's source & target:
graph.setEdgeAttribute('Martha', 'Jack', 'type', 'LIKES');
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the edge to update.
  * **attribute** <span class="code">string</span>: name of the attribute to set.
  * **value** <span class="code">any</span>: value to set.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attribute** <span class="code">string</span>: name of the attribute to set.
  * **value** <span class="code">any</span>: value to set.

### #.updateEdgeAttribute

Update the attribute of an edge using the provided function.

This method is very useful when performing tasks such as incrementing an attribute so you don't have to first fetch the former value to compute the next one.

Note that if the attribute is not yet setted, the passed value will be `undefined`.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Jack');
const edge = graph.addEdge('Martha', 'Jack', {weight: 1});

// Using the edge's key:
graph.updateEdgeAttribute(edge, 'weight', n => n + 1);

// Using the edge's source & target:
graph.updateEdgeAttribute('Martha', 'Jack', 'weight', n => n + 1);
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the edge to update.
  * **attribute** <span class="code">string</span>: name of the attribute to update.
  * **updater** <span class="code">function</span>: function used to perform the update.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attribute** <span class="code">string</span>: name of the attribute to update.
  * **updater** <span class="code">function</span>: function used to perform the update.

### #.removeEdgeAttribute

Remove the given edge's attribute altogether.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Jack');
const edge = graph.addEdge('Martha', 'Jack', {type: 'KNOWS'});

// Using the edge's key:
graph.removeEdgeAttribute(edge, 'type');

// Using the edge's source & target:
graph.removeEdgeAttribute('Martha', 'Jack', 'type');

graph.hasEdgeAttribute(edge, 'type');
>>> false
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the edge to update.
  * **attribute** <span class="code">string</span>: name of the attribute to set.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attribute** <span class="code">string</span>: name of the attribute to set.

### #.replaceEdgeAttributes

Completely replace one edge's attributes by the provided object.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Jack');
const edge = graph.addEdge('Martha', 'Jack', {type: 'KNOWS', weight: 1});

// Using the edge's key:
graph.replaceEdgeAttributes(edge, {type: 'LIKES', weight: 3});

// Using the edge's source & target:
graph.replaceEdgeAttributes('Martha', 'Jack', {type: 'LIKES', weight: 3}));
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the edge to update.
  * **attributes** <span class="code">object</span>: the new attributes.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **attributes** <span class="code">object</span>: the new attributes.

### #.mergeEdgeAttributes

Merge the current attributes of an edge with the provided object.

*Example*

```js
graph.addNode('Martha');
graph.addNode('Jack');
const edge = graph.addEdge('Martha', 'Jack', {type: 'KNOWS'});

// Using the edge's key:
graph.mergeEdgeAttributes(edge, {type: 'LIKES', weight: 3});

// Using the edge's source & target:
graph.mergeEdgeAttributes('Martha', 'Jack', {type: 'LIKES', weight: 3}));
```

*Arguments*

1. Using the key:
  * **edge** <span class="code">any</span>: the edge to update.
  * **data** <span class="code">object</span>: data to merge.
2. Using the source & target:
  * **source** <span class="code">any</span>: source of the edge.
  * **target** <span class="code">any</span>: target of the edge.
  * **data** <span class="code">object</span>: data to merge.

**Performance tip**: while this method is convenient, you'll be faster by using the [`#.setEdgeAttribute`](#setedgeattribute) method etc. in most cases and you'll enable renderers reacting to the graph's changes to act more efficiently, for instance.
