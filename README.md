## BiDirectional Hierarchical Sankey Diagram

This is a d3 javascript plugin/library for generating bidirectional hierarchial sankey diagrams

### Live Code Demonstration

For a a full demonstration of the use of this library:
http://bl.ocks.org/duhaime/3865371eea1bd32b36f53e63dabb6b72

### Overview

To Set the diagram properties:
```javascript
biHiSankey
  .nodeWidth(30) // sets the pixel width of all nodes (heights are variable, widths are fixed)
  .nodeSpacing(10) // sets the minimum vertical pixel spacing between nodes
  .linkSpacing(4) // sets the vertical pixel spacing between links
  .arrowheadScaleFactor(0.5) // Specifies the proportion of a link's stroke width that should be allowed for the marker at the end of the link e.g. an arrow
  .size([someWidth, someHeight]); // sets the width and height of the diagram in pixels
```

To (re)initialize the sankey diagram with data
```javascript
var someNodes = [
  {"type": "A", "id": 1, "parent": null, "name": "Node 1", depth: 0},
  {"type": "A", "id": 2, "parent": "1", "name": "Node 2"},
  {"type": "A", "id": 3, "parent": "1", "name": "Node 3"},
  {"type": "B", "id": 4, "parent": null, "name": "Node 4", depth: 1},
  {"type": "B", "id": 5, "parent": "4", "name": "Node 5"},
  {"type": "C", "id": 6, "parent": "5", "name": "Node 6"},
]
var someLinks = [
  {source: 3, target: 2, value: 20},
  {source: 2, target: 3, value: 90},
  {source: 3, target: 6, value: 40},
  {source: 6, target: 2, value: 70},
  {source: 6, target: 3, value: 10},
]

biHiSankey
  .nodes(someNodes) // pass in the nodes
  .links(someLinks) // pass in the nodes
  .initializeNodes(function (node) {
    // amend or add properties to each node as required
    // ...
  })
```

If two nodes `(n1, n2)` have different depths: `n1.depth < n2.depth` then the node `n1` will be placed to the left of `n2`

To (re)calculate the attributes of all nodes and links:
```javascript
biHiSankey.layout(20); // pass in a maximum number of iterations
```

To (re)calculate link paths and node heights but do not change the node positions:
```javascript
biHiSankey.relayout();

```

To return any of the previously set properties:
```javascript
biHiSankey.links();
biHiSankey.visibleLinks();
biHiSankey.linkSpacing();
biHiSankey.nodes();
biHiSankey.nodeWidth();
biHiSankey.nodeSpacing();
biHiSankey.size();
```

### License

BiHiSankey is released under the [MIT License](http://opensource.org/licenses/MIT).
