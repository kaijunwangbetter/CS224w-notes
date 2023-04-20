# PageRank

## Basic concepts of PageRank

- PageRank measures importance of nodes in a graph using the link structure of the web.
- Models a random web surfer using the stochastic adjacency matrix $M$
- PageRank solves $r=Mr$ where $r$ can be viewed as both the **principle enigenvector** of $M$ and as the **stationary distribution of a random walk** over the graph.

<big>
We can have a better understand of relationship between PageRank and Random Walk:

One surfer try to surf from one page, and he or she continues to surf endlessly. This kind of random walk can make the final distribution become stable. And the result is we have a stable web score table $r$ which $r=Mr$
</big>

## Power Iteration

## Some problems and methods

There are issues of **dead-ends** and **spider-traps**

- Dead-ends is a math problem(because matrix can add up to 1 but 0), one node without out link
- Spider-traps is not a math problem, one node without out link but self link

Solution: We can add random uniform teleportation:

$$
r_i=\sum_{i \rightarrow j}\beta\frac{r_i}{d_i} + (1-\beta)\frac{1}{N}
$$

## Matrix Factorization

We can simply use Matrix Factorization to get $Z$, which have $Z^TZ=A$(A is a adjacency matrix).

This kind of like the similarity of nodes.

And Deep Walk and node2vec can be also factorized in a similar way(but harder).
