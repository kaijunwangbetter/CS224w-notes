# Traditional featured-based methods

## Node

1. Degree counts #(edges) that a node touches.
2. Clustering coefficient counts #(triangles) that a node touches.
3. GDV(Graph Degree Vector) counts #(graphlets) that a node touches

## Link(Edge)

1. Distance-based features: use the shortest path between two nodes
2. Local neighborhood overlap: capture how many neighboring nodes are shared
3. Global neighborhood overlap: use global graph structure to score two nodes, Katz idnex as the count function

## Graph

1. Graphlet Kernel: use the idea of Bow as Bag-of-graphlets, record num of each kind graphlets as $\phi$ function(but computationally expensive)
2. Weisfeiler-Lehman Kernel: K-step color refinement to enrich colors, graph is represented as Bag-of-colors(which is computationally efficient)
