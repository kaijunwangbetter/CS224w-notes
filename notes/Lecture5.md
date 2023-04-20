# Message passing

## Background

- Main question today:
  Given a network with labels on some nodes, how do we assign labels to all other nodes in the network?

- Intuition: **Correlations** exist in networks(Similar nodes are connected)

- Key concept: **collective classification**(assign labels to all nodes in a network together)
- Three techniques:
  - Relational classigication
  - Iterative classification
  - Belief propagation

## Collective Classification

- Intuition: Homophily

- Markov Assumption: The label of one node only depend on the label of its neighbors.

- Usually 3 steps:
  - Local Classifier(initial label assignment)
  - Relational Classifier(Capture correlations)
  - Collective Inference(Propagate the correlation)

## Relational Classifiers

- Basic idea:
  Class probability $Y_v$ of node v is a weighted average of class probabilities of its neighbors.

### Step

- Initialize
  Labeled nodes with P=1, unlabeled nodes with P=0.5.
- Update
  For each node v and label c(e.g. 0 or 1)
  $$P(Y_v=c)=\frac{1}{\sum_{(v,u)\in E}A_{v,u}}\sum_{(v,u)\in E}A_{v,u}P(Y_u=c)$$
  However, convergence is not guaranteed.
  Model cannot use node feature information.
  Labeled nodes don't changed.

## Iterative classification

- Main idea: Classify node v based on its **attributes** $f_v$ as well as **labels** $z_v$ of neighbor set $N_v$
- Approch: Train two classifiers.
  - $\phi_1(f_v)$ Predict node label based on node feature vector $f_v$.
  - $\phi_2(f_v,z_v)$ Predict label based on node feature vector $f_v$ and summary $z_v$ of labels of v's neighbors.

### Step

- Classify based on node attributes alone.
- Apply classifier to test set.
- Iterate till convergence.
  - Update $z_v$ based on $Y-u$ for all $u \in N_v$
  - Update $Y_v$ based on the new $z_v(\phi_2)$
  - However, convergence is not guaranteed.

## (Loopy) Belief propagation

### Message Passing

- Basics:
  - Each node can only interact with its neighbors

### Notation

- Label-label potential matrix $\psi$
- Prior belief $\phi$
- $m_{i\rightarrow j}(Y_j)$ is i's message of j being in class $Y_j$
- $\mathcal{L}$ is the set of all classes/labels

### Algorithm

- Initialize all messages to 1
- Repeat for each node:
- $$m_{i \rightarrow j}(Y_j)=\sum_{Y_i \in \mathcal{L}}\psi(Y_i,Y_j)\phi_i(Y_i) \prod_{k \in N_i\\j}m_{k \rightarrow i}(Y_i) ,     \forall Y_j \in \mathcal{L}$$
- After convergence:
  - $b_i(Y_i)=$ node i's belief of being in class $Y_i$
  - $b_i(Y_i)=\phi_i(Y_i)\prod_{j \in N_i}m_{j \rightarrow i}{Y_j}, \forall Y_i \in \mathcal{L}$
