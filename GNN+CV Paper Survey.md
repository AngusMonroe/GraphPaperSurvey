# GNN+CV Paper Survey

## Social Relationship Understanding

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Deep Reasoning with Knowledge Graph for Social Relationship Understanding | https://arxiv.org/pdf/1807.00504.pdf | Gated GNN | propose an Graph Reasoning Model that unifies high-level knowledge graph with deep nn <br> a novel graph attention mechanism that explicitly reasons key contextual cues | https://github.com/HCPLab-SYSU/SR |


## Image Classification

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| FEW-SHOT LEARNING WITH GRAPH NEURAL NETWORKS | https://arxiv.org/pdf/1711.04043.pdf | GCN | cast few-shot learning as a supervised message passing task which is trained end-to-end using graph neural networks <br> match state-of-the-art performance on Omniglot and Mini-Imagenet tasks with fewer parameters <br> extend the model in the semi-supervised and active learning regimes |  https://github.com/vgsatorras/few-shot-gnn |
| Zero-shot Recognition via Semantic Embeddings and Knowledge Graphs | https://arxiv.org/pdf/1803.08035.pdf | GCN | propose an approach that uses both semantic embeddings and the categorical relationships to predict the classifiers |  |
| Multi-Label Zero-Shot Learning with Structured Knowledge Graphs | https://arxiv.org/pdf/1711.06526.pdf | Gated GNN | advance structured information and knowledge graphs for ML zero-shot learning |  |
| Rethinking Knowledge Graph Propagation for Zero-Shot Learning | http://openaccess.thecvf.com/content_CVPR_2019/papers/Kampffmeyer_Rethinking_Knowledge_Graph_Propagation_for_Zero-Shot_Learning_CVPR_2019_paper.pdf | GCN | exploits the hierarchical structure of the knowledge graph to perform zero-shot learning by efficiently propagating knowledge through the proposed dense connectivity structure <br> A novel weighting scheme for DGP where weights are learned based on the distance between nodes | https://github.com/cyvius96/adgpm |
| The More You Know: Using Knowledge Graphs for Image Classification | https://arxiv.org/pdf/1612.04844.pdf | Gated GNN | the introduction of the GSNN as a way of incorporating potentially large knowledge graphs into an end-to-end learning system that is computationally feasible for large graphs <br> a framework for using noisy knowledge graphs for image classification |  |


## Visual Question Answering

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Deep Reasoning with Knowledge Graph for Social Relationship Understanding | https://arxiv.org/pdf/1807.00504.pdf | Gated GNN | propose an Graph Reasoning Model that unifies high-level knowledge graph with deep nn <br> a novel graph attention mechanism that explicitly reasons key contextual cues | https://github.com/HCPLab-SYSU/SR |
| Graph-Structured Representations for Visual Question Answering | https://arxiv.org/pdf/1609.05600.pdf | Gated GNN | make use of an off-the-shelf language parsing tool by generating a graph representation of text that captures grammatical relationships, and by making this information accessible to the VQA model |  |
| Out of the box:
Reasoning with graph convolution nets for factual visual question answering | http://papers.nips.cc/paper/7531-out-of-the-box-reasoning-with-graph-convolution-nets-for-factual-visual-question-answering.pdf | Gated GNN | select a list of supporting facts in the KB by ranking GloVe embeddings <br> joint selection of the answer from a list of candidate answers |  |


## Object Detection

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Relation Networks for Object Detection | https://arxiv.org/pdf/1711.11575.pdf | Graph Attention Network | propose an adapted attention module for object detection which the primitive elements are objects instead of words | https://github.com/msracver/Relation-Networks-for-Object-Detection |
| Learning region features for object detection | http://openaccess.thecvf.com/content_ECCV_2018/papers/Jiayuan_Gu_Learning_Region_Features_ECCV_2018_paper.pdf | Graph Attention Network  | formulate the feature of each bin of the region as a weighted summation of image features on different positions over the whole image <br> a learnable module that represents the weights in terms of the RoI and image features |  |

## Interaction Detection

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Learning humanobject interactions by graph parsing neural networks | http://openaccess.thecvf.com/content_ECCV_2018/papers/Siyuan_Qi_Learning_Human-Object_Interactions_ECCV_2018_paper.pdf | GNN | incorporates structural knowledge and DNNs for learning and inference <br> addresses the HOI problem by jointly performing graph structure inference and message passing |  |
| Structural-rnn: Deep learning on spatio-temporal graphs | http://openaccess.thecvf.com/content_cvpr_2016/papers/Jain_Structural-RNN_Deep_Learning_CVPR_2016_paper.pdf | GNN | proposed a generic method for casting an arbitrary st-graph as a rich, scalable, and jointly trainable RNN mixture | http://asheshjain.org/srnn |

## Region Classification

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Iterative visual reasoning beyond convolutions | https://arxiv.org/pdf/1803.11189.pdf | Graph CNN | learn from structured information in the form of knowledge bases for visual recognition |  |

## Semantic Segmentation

| title | link | base model | contribution | code |
| --- | --- | --- | --- | --- |
| Semantic Object Parsing with Graph LSTM |  | Graph LSTM | take each arbitrary-shaped superpixel as a semantically consistent node, and adaptively construct an undirected graph for each image, where the spatial relations of the superpixels are naturally used as edges |  |
| Interpretable structure-evolving lstm | https://arxiv.org/pdf/1703.03055.pdf | Graph LSTM | further learn the intermediate interpretable multi-level graph structures in a progressive and stochastic way from data during the LSTM network optimization |  |
| Large-scale point cloud semantic segmentation with superpoint graphs | https://arxiv.org/pdf/1711.09869.pdf | Gated GNN | PointNets for superpoint embedding and graph convolutions for contextual segmentation <br> a novel, more efficient version of EdgeConditioned Convolutions as well as a new form of input gating in Gated Recurrent Units | https://github.com/loicland/superpoint_graph |
| Dynamic graph cnn for learning on point clouds | https://arxiv.org/pdf/1801.07829.pdf | Graph CNN | present a novel operation for learning from point clouds, EdgeConv, to better capture local geometric features of point clouds while still maintaining permutation invariance | https://github.com/WangYueFt/dgcnn |
| 3d graph neural
networks for rgbd semantic segmentation | http://openaccess.thecvf.com/content_ICCV_2017/papers/Qi_3D_Graph_Neural_ICCV_2017_paper.pdf | GNN |  builds a k-nearest neighbor graph on top of 3D point cloud. Each node in the graph corresponds to a set of points and is associated with a hidden representation vector initialized with an appearance feature extracted by a unary CNN from 2D images. |  |

## Miscellaneous

| title | link | domain |
| --- | --- | --- |
| Can GCNs Go as Deep as CNNs? | https://arxiv.org/pdf/1904.03751 | train very deep GCNs <br> point cloud semantic segmentation |
| LEARNING LOCALIZED GENERATIVE MODELS FOR 3D POINT CLOUDS VIA GRAPH CONVOLUTION | https://openreview.net/pdf?id=SJeXSo09FQ | unsupervised problem of a generative model exploiting graph convolution |
| 3D Graph Neural Networks for RGBD Semantic Segmentation | http://www.cs.toronto.edu/~rjliao/papers/iccv_2017_3DGNN.pdf | RGBD semantic segmentation |
| Weisfeiler and Leman Go Neural: Higher-order Graph Neural Networks | https://arxiv.org/pdf/1810.02244v2.pdf | graph classification <br> characterization of social networks and molecule graphs |
| How Powerful are Graph Neural Networks? | https://arxiv.org/pdf/1810.00826.pdf | graph classification |
| Out of the Box: Reasoning with Graph Convolution Nets for Factual Visual Question Answering | https://arxiv.org/abs/1811.00538 | `fact-based' visual question answering |
| FEW-SHOT LEARNING WITH GRAPH NEURAL NETWORKS | https://arxiv.org/pdf/1711.04043.pdf | few-shot learning |
| Zero-shot Recognition via Semantic Embeddings and Knowledge Graphs | https://arxiv.org/pdf/1803.08035.pdf | Zero-shot learning |
