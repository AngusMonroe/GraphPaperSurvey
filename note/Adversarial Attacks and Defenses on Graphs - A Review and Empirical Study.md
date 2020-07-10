# Adversarial Attacks and Defenses on Graphs: A Review and Empirical Study

![截屏2020-07-09 11.43.18.png](https://i.loli.net/2020/07/09/ECf7mxwJnRzHQNq.png)

## Link
https://arxiv.org/pdf/2003.00653.pdf

## Key Points

1. categorize existing attack methods from various perspectives and review representative algorithms.
2. classify existing countermeasures according to their defense strategies and give a review on representative algorithms for each category.
3.  perform empirical studies based on the repository we developed that provide comprehensive understandings on graph attacks and defenses
4. discuss some promising future directions

## Outline

### Preliminaries and Definitions

Use $G = (V, E)$ to denote the structure of a graph where $V=\left\{v_{1}, \ldots, v_{N}\right\}$ is the set of N nodes and $E=\left\{e_{1}, \ldots, e_{K}\right\}$ is the edge set. Use $\mathbf{A} \in\{0,1\}^{N \times N}$ to denote the adjacency matrix of $G$, where each entry $A_{ij}=1$ means nodes $v_i$ and $v_j$ are connected in $G$. Use $\mathbf{X} \in \mathbb{R}^{N \times D}$ to denote the node attribute matrix where$D$ is the dimension of the node feature vectors.Thus, graph data can be denoted as $F=(A, X)$. Use $f_\theta$ with parameters $\theta$ to denote the learning models in this survey.

![截屏2020-07-09 17.59.42.png](https://i.loli.net/2020/07/09/YmKLuA3PCRjliGq.png) 

![截屏2020-07-10 10.01.42.png](https://i.loli.net/2020/07/10/zQfRKYEPIS3bkGj.png)

The aimof adversarial attacks is to maximize the loss value of the model in order eo get wrong prediction. The problem of node-level graph adversarial attacks can be stated as: 

$$\max \mathcal{L}_{a t k}\left(f_{\theta}(\hat{G})\right)=\sum_{u \in V_{t}} \ell_{a t k}\left(f_{\theta^{*}}(\hat{G})_{u}, y_{u}\right)$$
$$s.t., \quad \theta^{*}=\arg \min _{\theta} \mathcal{L}_{\text {train}}\left(f_{\theta}\left(G^{\prime}\right)\right)$$

where $G^\prime$ can either be $G$ or $\hat{G}$. Bot that $\hat{G}$ is chosen from a constrained domain $\Phi(G)$. Gifen a fixed perturbation budget $\Delta$, a typical $\Phi(G)$ can be implemented as $\|\hat{\mathbf{A}}-\mathbf{A}\|_{0}+\|\hat{\mathbf{X}}-\mathbf{X}\|_{0} \leq \Delta$.

### Taxonomy of Graph Advversarial Attacks

#### Attacker's Capacity

- Evasion Attack: Attacking happens after the GNN model is trained or in the test phase. The model is fixed, and the attacker cannot change the model parameter or structure. The attacker performs evasion attack when $G^\prime = G$.
- Poisoning Attack: Attacking happens before the GNN model is trained. The attacker can add “poisons” into the model training data, letting trained model have malfunctions. It is the case when $G^\prime = \hat{G}$.

#### Perturbation Type

- Modifying Feature: Attackers can slightly change the node features while maintaining the
graph structure.
- Adding or Deleting Edges: Attackers can add or delete edges under certain budget of total
actions.
- Injecting Nodes: Attackers can insert fake nodes to the graph, and link it with some benign
nodes in the graph.

#### Attacker's Goal

- Targeted Attack: There is a small set of test nodes. The attacker aims to let the trained model misclassify these test samples. It is the case when $V_{t} \subset V$. (3). We can further divide targeted attacks into (1) direct attack where the attacker directly modifies the features
or edges of the target nodes and (2) influencer attack where the attacker can only manipulate
other nodes to influence the targets.
- Untargeted Attack: The attacker aims to insert poisons to let the trained model have bad
overall performance on all test data. It is the case when $V_{t} = V$.

#### Attacker's Knowledge

- White-box Attack: All information about the model parameters, training input (e.g, adjacency matrix and attribute matrix) and the labels are given to the attacker.
- Gray-box Attack: The attacker only has limited knowledge about the victim model. For example, the attacker cannot access the model paramerters but can access the training labels. Then it can utilize the training data to train surrogate models to estimate the information from victim model.
- Black-box Attack: The attacker does not have access to the model’s parameters or training labels. It can access the adjacency matrix and attribute matrix, and do black-box query for output scores or labels.

### Graph Adversarial Attacks

![截屏2020-07-10 11.55.13.png](https://i.loli.net/2020/07/10/42iQRdg7vHG3aZX.png)

#### White-box Attacks

- Targeted Attack
	- **FGA**: extracts the link gradient information from GCN, and then greedily selects the pair of nodes with maximum absolute gradient to modify the graph iteratively.
	- **Genetic algorithm based Q-Attack**: attack a number of community detection algorithms.
	- **Iterative aradient attack (IGA)**: based on the gradient information in the trained graph auto-encoder, which is introduced to attack link perdiction.
	- **Knowledge graph embedding attack**: including Direct Delete Attack, Direct Adding Attack and Indirect Attack.
	- **IG-JSMA**: use integrated gradient to better search for adversarial edge and feature perturbations.
	- **GUA**: finds a set of anchor nodes (bad actor) to mislead the classification of all nodes in the graph through flipping the connections between the anchors and the target node.

- Untargeted Attack
	- **topology attack**: constructs a binary symmetric
perturbation matrix and minimizes the predefined attack loss given a finite budget of edge perturbations.

#### Gray-box Attacks

- Targeted Attack
	- **Nettack**: first selects possible perturbation candidates not violating degree distribution and feature co-occurrence of the original graph. Then it greedily chooses the perturbation that has the largest score to modify the graph. 

- Untargeted Attack
	- **Metsttack**: treats the graph structure matrix as a hyper-parameter and use  a greed approach to select the perturbation based on the meta gradient.
	- **nodel injection poison attack (NIPA)**: inject fake nodes into graph data.

#### Black-box Attacks

- Targeted Attack
	Reinforcement learning mostly.
	- **RL-S2V**: model the attack procedure as a Markov Decision Process (MDP) and the attacker is allowed to modify m edges to change the predicted label of the target node $u$. For every time step, the attacker can choose to add or remove an edge from the graph. The model gives non-zero reward to the attacker at the end of the MDP. The Q-learning algorithm is adopted to solve the MDP and guide the attacker to modify the graph.
	- **GF-Attack**: formulate the connection between the graph embedding method and general graphsognal process with graph filter and construct the attacker based on the graph filter and attribute matrix.

- Untargeted Attack
	- **ReWatt**: adopts the rewiring operation instead of simply adding/deleting an edge in one singlemodification to make perturbation more unniticeable. One rewiring operation involves three nodes $v_1$, $v_2$ and $v_3$, where ReWatt removes the existing edge between $v_1$ and $v_2$ and connects $v_1$ and $v_3$. ReWatt also constrains $v_3$ to be the 2-hop neighbor of $v_1$ to make perturbation smaller. 

### Countermreasures Against Graph Adversarial

#### Adversarial Training

The main idea of adversarial training is to inject adversarial examples into the training set such that the trained model can correctly classify the future adversarial examples. 

![截屏2020-07-10 21.12.18.png](https://i.loli.net/2020/07/10/ni6BZka58XxgmEw.png)

The min-max optimization problem indicates that adversarial training involves two process: (1) generating perturbations that maximize the prediction loss and (2) updating model parameters that minimize the prediction loss.

To overcome the problem that the perturbation generation on $A$ and $X$ in separately and perturb the graph structure is not easy due to its discreteness,  instead of generating perturbation on the input, a latent adversarial training method injects perturbations on the first hidden layer.

$$\min _{\theta} \max _{\delta \in \mathcal{P}} \mathcal{L}_{\operatorname{train}}\left(f_{\theta}\left(G ; \mathbf{H}^{(1)}+\delta\right)\right)$$

where $\mathbf{H}^{(1)}$ denotes the representation matrix of the first hidden layer and $\delta \in \mathcal{P}$ is some perturbation on $\mathbf{H}$. It is noted that the hidden representation is continuous and it incorporates the information from both graph structure and node attributes.

#### Detecting Adversarial Perturbations

Four methods to distinguish adversarial edges or nodes from the clean ones including

1. link prediction
2. sub-graph link prediction
3. graph generation models
4. outlier detection

**GraphSAC**: introduces a method to randomly draw subsets of nodes, and relies on graph-aware criteria to judiciously filter out contaminated nodes and edges before employing a semi-supervised learning (SSL) module. The proposed model can be used to detect different anomaly generation models, as well as adversarial attacks.

#### Certifiable Robustness

To find nodes in the graph are safe under the risk of any admissible perturbation, we could try to find an upper bound $U(v)$ of the maximized margin loss.

$$U \geq \max _{\hat{\mathbf{X}} \in \mathcal{X}}\left(f_{\theta}(\hat{\mathbf{X}}, \mathbf{A})\left[y_{v}\right]-f_{\theta}(\hat{\mathbf{X}}, \mathbf{A})[y]\right)$$

The Upper bound $U$ is called the certificate of node $v$. . During the test phase, they calculate the certificate for all test nodes, thus they can know how many nodes in a graph is absolutely safe under attributes perturbation. Moreover, this certificate is trainable, directly minimizing the certificates will help more nodes become safe.

If the attacker only manipulates the graph structure, we could t derives the robustness certificates as a linear function of personalized PageRank, which makes the optimization tractable.

#### Graph Purification

Purification methods first purify the perturbed graph data and then train the GNN model on the purified graph. By this way, the GNN model is trained on a clean graph.

Two empirical observations of the attack methods: (1) Attackers usually prefer adding edges over removing edges or modifying features and (2) Attackers tend to connect dissimilar nodes. We could eliminating the edges whose two end nodes have small Jaccard Similarity to defense the attack.

Nettack proposes to purify the perturbed adjacency matrix by using truncated SVD to get its low-rank approximation. it further shows that only keeping the top 10 singular values of the adjacency matrix is able to defend Nettack and improve the performance of GNNs.

#### Attention Mechanism

Attentionbased defense methods aim to train a robust GNN model by penalizing model’s weights on adversarial edges or nodes. When aggregating the information from neighbor nodes, it applies an attention mechanism to penalize the nodes with high variance.

To improve the robustness of one target GNN model, it is beneficial to include the information from other clean graphs, which share the similar topological distributions and node attributes with the target graph.

### Emporocal Study

![截屏2020-07-10 22.16.36.png](https://i.loli.net/2020/07/10/9LfnskOR8dPw2z1.png)

It can be observed from the table:

- Attackers favor adding edges over deleting edges.
- Attacks are likely to increase the rank of the adjacency matrix.
- Attacks are likely to reduce the connectivity of a graph. The clustering coefficients of a perturbed graph decrease with the increase of the perturbation rate.

![截屏2020-07-10 22.17.00.png](https://i.loli.net/2020/07/10/yzRNBQWgUT4cI61.png)

We can make the following observations from the figures:

- Attackers tend to connect nodes with different labels and dissimilar features.
- Attackers tend to remove edges from nodes which share similar features and same label.

### Future Directions

- Imperceptible perturbation measure. Different from image data, humans cannot easily tell whether a perturbation on graph is imperceptible or not. The $\ell_{0}$ norm constraint on perturbation is definitely not enough. Currently only very few existing work study this problem, thus finding concise perturbation evaluation measure is of great urgency.
- Different graph data. Existing works mainly focus on static graphs with node attributes. Complex graphs such as graphs with edge attributes and dynamic graphs are not well-studied yet.
- Existence and transferability of graph adversarial examples. There are only a few works discussing about the existence and transferability of graph adversarial examples. Studying this topic is important for us to understand our graph learning algorithm, thus helping us build robust models.
- Graph structure learning. By analyzing the attacked graph, we find that attacks are likely to change certain properties of graphs. Therefore, we can learn a graph from the poisoned graphs by exploring these properties to build robust GNNs.
