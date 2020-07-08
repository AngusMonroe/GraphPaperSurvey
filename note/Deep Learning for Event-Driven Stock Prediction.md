# Deep Learning for Event-Driven Stock Prediction

![截屏2020-07-08 15.43.55.png](https://i.loli.net/2020/07/08/dPb2jtLOiHouBgw.png)

## Link
https://www.ijcai.org/Proceedings/15/Papers/329.pdf

## Key Points
- Use event extracted from news text to train a neural tensor network.
- Use CNN model short-term and ling-term influence of events on stock price movement.

## Outline

### Background

Pioneering work mainly uses simple features from news documents, such as bags-of-words, noun phrases, and named entities. These features do not capture structured relations.

For example, representing the event “Microsoft sues Barnes & Noble.” using term-level features {“Microsoft”, “sues”, “Barnes”, “Noble”} alone, it can be difficult to accurately predict the price movements of Microsoft Inc. and Barnes & Noble Inc., respectively, as the unstructured terms cannot differentiate the accuser (“Microsoft”) and defendant (“Barnes & Noble”).

![截屏2020-07-08 16.19.34.png](https://i.loli.net/2020/07/08/qhUbQdG6kIcLXHS.png)

The performance of daily predic- tion is better than weekly and monthly prediction. Despite the relatively weaker effects of long-term events, the volatility of stock markets is still affected by them. However, little previous work quantitatively models combined short-term and long-term effects of events. 

### Model

#### Event Representation and Extraction

Represent an event as a tuple $E = (O_1,P,O_2,T)$,where $P$ is the action, $O_1$ is the actor and $O_2$ is the object on which the action is performed. $T$ is the timestamp of the event.

For example, the event “Jan 13, 2014 - Google Acquires Smart Thermostat Maker Nest for \$3.2 billion.” is modeled as: $(Actor = Google, Action = acquires, Object = Nest, Time = Jan 13, 2014)$.

Extract structured events from free text using Open IE technology and dependency parsing.

#### Event Embedding

Our goal is to automatically learn embeddings for structured event tuples $E = (O_1, P, O_2)$, which draw more fundamental relations between events, even if they do not share the same action, actor or object.

Different with representation of knowledge tuple, the relation type in this task in unlimited, which means we can't train a specific model for each event type. To address this issue, we represent the action $P$ as a vector, which shares the dimensionality with event arguments.

The relation in database embedding is inter changeable, but the event relation is not interchangeable. So they first use $O_1T_1P$ and  $PT_2O_2$ to construct two role-dependent embeddings $R_1$ and $R_2$. And then use $R_1T_3R_2$ as the representation $U$ of $E=(O_1, P, O_2)$.

![截屏2020-07-08 17.26.21.png](https://i.loli.net/2020/07/08/X9pCiwbjks7t4DL.png)

$$R_{1}=f\left(O_{1}^{T} T_{1}^{[1: k]} P+W\left[\begin{array}{c}O_{1} \\ P\end{array}\right]+b\right)$$

$R_2$ and $U$ are computed in the same way as $R_1$.

Since the event is pretty sparse, some corrupted event tuples $E^r=(O_1^r, P, O_2)$ have been constructed by replace $O_1$ by a random word in the dictionary. The loss have been calculated by:

$$\operatorname{loss}\left(E, E^{r}\right)=\max \left(0,1-f(E)+f\left(E^{r}\right)\right)+\lambda\|\Phi\|_{2}^{2}$$

If the loss is equal to zero, the algorithm continues to process the next event tuple. Otherwise, the parameters are updated to minimize the loss using the standard back-propagation (BP) algorithm. The it- eration number N is set to 500.

![截屏2020-07-08 18.05.31.png](https://i.loli.net/2020/07/08/y4kWcKVAp5ht3JD.png)

####Deep Prediction Model

We model long-term events as events over the past month, mid-term events as events over the past week, and short-term events as events on the past day of the stock price change. 

![截屏2020-07-08 18.05.15.png](https://i.loli.net/2020/07/08/f1rImROJZvNw4os.png)

For long-term (left) and mid-term (mid- dle) news, the narrow convolution operation is used to com- bine l (l = 3) neighbour events. It can be viewed as feature extraction based on sliding window, which can capture local information through combinations of vectors in a window.

Use a max pooling layer on top of the convolutional layer, which forces the network to retain only the most useful local features pro- duced by the convolutional layer.

For short-term events, we obtain the feature vector $V$ s by directly using its averaged event embeddings $U^s$. The feature layer is the combination of long-term, mid-term and short- term feature vectors $V^C =(V^l,V^m,V^s)$.

To correlate the feature vector $V^C$ and stock prices, we use a feedforward neural network with one hidden layer and one output layer. 

###Experiment

#### Dataset

Use financial news from Reuters and Bloomberg over the period from October 2006 to November 2013 for training.

Conduct experiment on Standard & Poor’s 500 stock (S&P 500).

Metric: accuracy (Acc), Matthews Correlation Cofficient (MCC) and profitability.

#### Baseline

- bags-of-words + SVM (Luss and d’Aspremont [2012])
- Open IE + feedforward network (Ding et al. [2014]) (E-NN)

#### Result

![截屏2020-07-08 18.29.31.png](https://i.loli.net/2020/07/08/2I5yRbYa7gwG4OZ.png)

![截屏2020-07-08 18.31.39.png](https://i.loli.net/2020/07/08/SP4QITVAfYNaRe1.png)

## Questions
