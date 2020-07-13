# Adversarial Attacks & Defenses Survey

## Definition

Use $G = (V, E)$ to denote the structure of a graph where $V=\left\{v_{1}, \ldots, v_{N}\right\}$ is the set of N nodes and $E=\left\{e_{1}, \ldots, e_{K}\right\}$ is the edge set. Use $\mathbf{A} \in\{0,1\}^{N \times N}$ to denote the adjacency matrix of $G$, where each entry $A_{ij}=1$ means nodes $v_i$ and $v_j$ are connected in $G$. Use $\mathbf{X} \in \mathbb{R}^{N \times D}$ to denote the node attribute matrix where$D$ is the dimension of the node feature vectors.Thus, graph data can be denoted as $F=(A, X)$. Use $f_\theta$ with parameters $\theta$ to denote the learning models in this survey.

![截屏2020-07-09 17.59.42.png](https://i.loli.net/2020/07/09/YmKLuA3PCRjliGq.png) 

![截屏2020-07-10 10.01.42.png](https://i.loli.net/2020/07/10/zQfRKYEPIS3bkGj.png)

The aimof adversarial attacks is to maximize the loss value of the model in order eo get wrong prediction. The problem of node-level graph adversarial attacks can be stated as: 

$$\max \mathcal{L}_{a t k}\left(f_{\theta}(\hat{G})\right)=\sum_{u \in V_{t}} \ell_{a t k}\left(f_{\theta^{*}}(\hat{G})_{u}, y_{u}\right)$$
$$s.t., \quad \theta^{*}=\arg \min _{\theta} \mathcal{L}_{\text {train}}\left(f_{\theta}\left(G^{\prime}\right)\right)$$

where $G^\prime$ can either be $G$ or $\hat{G}$. But that $\hat{G}$ is chosen from a constrained domain $\Phi(G)$. Given a fixed perturbation budget $\Delta$, a typical $\Phi(G)$ can be implemented as $\|\hat{\mathbf{A}}-\mathbf{A}\|_{0}+\|\hat{\mathbf{X}}-\mathbf{X}\|_{0} \leq \Delta$.

## Taxonomy

- Attacker's Capacity

	- Evasion Attack
	- Poisoning Attack

## Perturbation Type

- Modifying Feature
- Adding or deleting Edges
- Injecting Nodes

## Attacker's Goal

- Targeted Attack
- Untargeted Attack

## Attacker's Knowledge

- White-box Attack
- Gray-box Attack
- Black-box Attack

## Papers

### Survey

- **[Adversarial Attacks and Defenses on Graphs:
A Review and Empirical Study](./note/AdversarialAttacksandDefensesonGraphs-AReviewandEmpiricalStudy.md)** (*arXiv*) [Paper](https://arxiv.org/pdf/2003.00653.pdf)

### White-box Attacks

- **Fast Gradient Attack on Network Embedding** (FGA) (*arXiv*)  [Paper](https://arxiv.org/pdf/1809.02797.pdf)

	Designed an adversarial network generator based on the GCN gradient, select the pair of notes of the maximum absolute gradient to update the adversarial network.
	
- **GA Based Q-Attack on Community Detection** (*TCSS*)  [Paper](https://arxiv.org/pdf/1811.00430.pdf)

	![截屏2020-07-13 11.54.17.png](https://i.loli.net/2020/07/13/fFrmMEqRX4bwgSh.png)

- **Link prediction adversarial attack** (IGA) (*arXiv*) [Paper](https://arxiv.org/pdf/1810.01110.pdf)

	Calculate gradient for the target link, add the link with maximum gradient and delete the link with minimum gradient.

	![截屏2020-07-13 12.36.27.png](https://i.loli.net/2020/07/13/ndzQjPsTVHoFvgY.png)
	
- **Towards Data Poisoning Attack against Knowledge Graph Embedding** (*IJCAI'19*) [Paper](https://www.researchgate.net/profile/Tianhang_Zheng/publication/332751020_Towards_Data_Poisoning_Attack_against_Knowledge_Graph_Embedding/links/5cd079a7a6fdccc9dd91e1cb/Towards-Data-Poisoning-Attack-against-Knowledge-Graph-Embedding.pdf)

	Put forward a n optimal embedding shifting vector and use this vector to caculate the perturbation benefit scoreof specific candidate to add/delete.
	
- **Adversarial Examples on Graph Data: Deep Insights into Attack and Defense** (*arXiv*) [Paper](https://arxiv.org/pdf/1903.01610.pdf)

	use integrated gradient to better search for adversarial edge and feature perturbations.
	
	![截屏2020-07-13 17.57.03.png](https://i.loli.net/2020/07/13/uM7CsrUb1Jknawj.png)
	
- **Graph Universal Adversarial Attacks: A Few Bad Actors Ruin Graph Learning Models** (GUA) (*arXiv*) [Paper](https://arxiv.org/pdf/2002.04784.pdf)

	finds a set of anchor nodes (bad actor) to mislead the classification of all nodes in the graph through flipping the connections between the anchors and the target node.
	
	![截屏2020-07-13 18.36.30.png](https://i.loli.net/2020/07/13/cY3gu4lCnFkLAXD.png)
	
- **Topology attack and defense for graph neural networks: An optimization perspective** (*IJCAI'19*) [Paper](hhttps://arxiv.org/pdf/1906.04214.pdf)

	constructs a binary symmetric perturbation matrix and minimizes the predefined attack loss given a finite budget of edge perturbations. Yields projected gradient descent (PGD) topology attack for pre0defined GNN and min-max topology attack for re-trainable GNN.

### Gray-box Attacks

- **Practical Attacks Against Graph-based Clustering** (*CCS'17*) [Paper](https://arxiv.org/pdf/1708.09056.pdf) 
	
	first selects possible perturbation candidates not violating degree distribution and feature co-occurrence of the original graph. Then it greedily chooses the perturbation that has the largest score to modify the graph. 

- **Adversarial attacks on graph neural networks via meta learning** (*ICLR'19*) [Paper](https://arxiv.org/pdf/1902.08412.pdf)

	treats the graph structure matrix as a hyper-parameter and use  a greed approach to select the perturbation based on the meta gradient.
	
- **Node injection attacks on graphs via reinforcement learning** (NIPA)  (*arXiv*) [Paper](https://arxiv.org/pdf/1909.06543.pdf)

	inject fake nodes into graph data. put forward a hierarchical Q-learning based method that can be executed by an adversary to eectively perform the poisoning attack.

### Black-box Attacks

Reinforcement learning mostly.
 
- **Adversarial attack on graph structured data** (RL-S2V)  (*ICML'18*) [Paper](https://arxiv.org/pdf/1806.02371.pdf) 

	model the attack procedure as a Markov Decision Process (MDP) and the attacker is allowed to modify m edges to change the predicted label of the target node $u$. For every time step, the attacker can choose to add or remove an edge from the graph. The model gives non-zero reward to the attacker at the end of the MDP. The Q-learning algorithm is adopted to solve the MDP and guide the attacker to modify the graph.

- **The General Black-box Attack Method for Graph Neural Networks** (GF-Attack)  (*arXiv*) [Paper](https://arxiv.org/pdf/1908.01297v1.pdf) 

	formulate the connection between the graph embedding method and general graphsognal process with graph filter and construct the attacker based on the graph filter and attribute matrix.

- **Attacking graph convolutional networks via rewiring** (ReWatt)  (*arXiv*) [Paper](https://arxiv.org/pdf/1906.03750.pdf) 

	adopts the rewiring operation instead of simply adding/deleting an edge in one singlemodification to make perturbation more unniticeable. One rewiring operation involves three nodes $v_1$, $v_2$ and $v_3$, where ReWatt removes the existing edge between $v_1$ and $v_2$ and connects $v_1$ and $v_3$. ReWatt also constrains $v_3$ to be the 2-hop neighbor of $v_1$ to make perturbation smaller. 

## Other resources

[Graph Adversarial Learning Literature](https://github.com/safe-graph/graph-adversarial-learning-literature)