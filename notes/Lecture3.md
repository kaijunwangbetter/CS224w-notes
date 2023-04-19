<font face="Times New Roman">

# Embedding

## Node Embeddings

- Encoder + Decoder Framework.

- Shallow encoder: embedding lookup.
  Deep encoder: GNNs.

- Decoder: based on node similarity.
  Objective: maximize $z_v^Tz_u$ for node pairs $(u,v)$ that are similar.

**This is a unsupervised way of learning node embeddings**

## Random Walk Approaches for Node Embeddings

1. Run shorted fixed-length random walks starting from each node on the graph.
2. For each node $u$ collect $N_R(u)$.
3. Optimize embeddings using SGD.
   $$\mathcal L = \sum_{u\in V}\sum_{v\in N_R(u)}- log(P(v|z_u)$$

## node2vec

<big>
The difference between Deep Walk and node2vec:

1. How set of neighboring nodes is defined.
2. How the random walk is defined.
   </big>

### Idea:

use flexible, biased random walks that can trade off between **local** and **global** views of the network.

Two hyperparameter:

- Return parameter $p$:
  - Return back to the previous node
- In-out parameter $q$:
  - Moving outwards(DFS) vs. inwards(BFS)
  - Intuitively, q is the ratio of BFS vs. DFS

### Biased $2^{nd}-order$ random walks explore neighborhoods:

Insight:
Neighbors of w can only be:

- farther from original node s. $P=\frac{1}{q} $
- same distance to s. $P=1$
- back to s. $P=\frac{1}{p} $

### Algorithim

1. Compute random walk probabilities.
2. Simulate r random walks of length l starting from each node u.
3. Optimize the node2vec objective using SGD.

Linear-time complexity and all 3 steps are indevidually parallelizable.

## Embedding Entire Graphs

1. Embed nodes and sum/avg them
2. Create super-virtual-node that spans the (sub)gtaph and then embed that node
3. Anonymous Walk Embeddings
   - Sample the anon. Walk and represent the graph as fractoin of times each anon walk occurs
   - Embed anonymous walks, concatenate their embeddings to get a graph embedding.
