# FedMP: Federated Learning through Adaptive Model Pruning in Heterogeneous Edge Computing

## Abstract

Federated learning (FL) has been widely adopted to train machine learning models over massive distributed data sources in edge computing. However, the existing FL frameworks usually suffer from the difficulties of **resource limitation** and **edge heterogeneity**. Herein, we design and implement FedMP, an efficient FL framework through **adaptive model pruning**. We **theoretically** analyze the impact of **pruning ratio** on model training performance, and propose to employ a **Multi-Armed Bandit** based online learning algorithm to adaptively determine different pruning ratios for heterogeneous edge nodes, even **without any prior knowledge** of their computation and communication capabilities. With adaptive model pruning, FedMP can not only **reduce resource consumption** but also achieve promising **accuracy**. To prevent the diverse structures of pruned models from affecting the training convergence, we further present a new parameter synchronization scheme, called **Residual Recovery Synchronous Parallel (R2SP)**, and provide a theoretical convergence guarantee. Extensive experiments on the classical models and datasets demonstrate that FedMP is effective for different heterogeneous scenarios and data distributions, and can provide up to 4.1× speedup compared to the existing FL methods.



## Introduction

- **cloud computing**?
  - privacy leak
  - network congestion
  - high transmission delay
- **parameter server** based framework?
  - scarce communication bandwidth
  - limited on-edge resources
  - heterogeneous edge nodes
- solutions such as **quantization** and **compression**?
  - dedicated to alleviating the **total communication cost** & do not essentially **reduce the model complexity (computation & storage overhead)**
    - communication: reduce the frequency of global aggregation, gradient sparsification & quantization
  - ignore **device heterogeneity (different computation & storage capabilities)**

![image-20221202114130978](https://raw.githubusercontent.com/ailianligit/ailianligit.github.io/main/images/202212/20221208_1670498895.png)

- existing pruning methods?
  - **unstructured pruning**
    - removes the unimportant **weights** (i.e., the connections between the neurons)
      - does not efficiently reduce the computation time since most removed weights are from the fully-connected layers, but the computation cost is concentrated in the convolutional layers   
    - a high level of **parameter sparsity** and irregularization of the resulting sparse matrix
      - difficult to compress the parameters in memory
      - specialized hardware/libraries are required to accelerate the model training
  - structured pruning
    - remove some unimportant **model structures** (e.g., convolutional filters) without introducing **sparsity**
    - a sub-figure or sub-model of the original neural network
    - contains **fewer parameters** and helps **reduce both communication and computation overhead**
  - proposed for **centralized model training**
  - there is **no data on the PS for model pre-training**
- FedMP
  - **adaptive model pruning**: reduce **computation and communication overhead**
  - a **Multi-Armed Bandit (MAB)** based online learning algorithm: determine the **pruning ratios** for the workers even **without knowing any prior knowledge of their capabilities**, adaptively learn the **quantitative relationship among pruning ratio, resource consumption and model performance** to achieve the **trade-off between efficiency and accuracy**
  - **Residual Recovery Synchronous Parallel (R2SP)**: **recovers the sub-models** with diverse structures before model aggregation and **ensures comprehensive model updates** during the training process
  - effective for **different heterogeneous scenarios and data distributions**, up to 4.1× speedup compared to the **existing FL methods**



## Proposed Framework

<img src="https://raw.githubusercontent.com/ailianligit/ailianligit.github.io/main/images/202212/20221212_1670851392.png" alt="image-20221212212255538" style="zoom: 50%;" />

### Adaptive Model Pruning

- pruning ratio: $\alpha_n^k$ for each worker $n$ in round $k$
- **distributed** model pruning
- **structured pruning**
- every layer uses the **same pruning ratio**
- **filter’s score**: the sum of the absolute kernel weights
- **neuron’s score**: the sum of the absolute weights that the neuron is connected to
  - low-weight connections have a weak effect on model accuracy

- When **the filters with their feature maps** are pruned, the **corresponding channels of filters in the next layer** are also removed
- if **a convolutional layer** is pruned, **the weights of the subsequent batch normalization layer** are removed too

### Local Training

- The larger the pruning ratio is (i.e., more global model parameters are pruned), the fewer **CPU cycles** it requires to process a data sample.

### Model Aggregation

- **R2SP**: recover the sub-models
  - **Sparse model $\textbf{x}_n^k$**: has the same network structure as the global model except that some parameters to be (**logically**) pruned are set to 0
    - **Residual model $\overline{\textbf{x}}_n^k$**: global model $\textbf{x}^k$ - sparse model $\textbf{x}_n^k$
    - further reduce the memory overhead: **quantize** each parameter in residual models with fewer bits

  - **Sub-model $\hat{\textbf{x}}_n^k$**: has a more compact structure compared to the sparse model, as some parameters are pruned **physically**
    - the **indexes** (binary vector) of the remaining parameters also need to be recorded for each worker $n$

  - each model parameter has a chance to be trained

- aggregating the recovered models: derive an updated global model

### Convergence Analysis

- Assumptions of loss function:
  - **Smoothness**: Each function $f_n(x)$ is smooth with modulus $L$
  - **Bounded variances** and **second moments**
- **pruning error**: $Q^k_n\triangleq \mathbb{E}\left[\lVert \textbf{x}^k-\textbf{x}^k_n\rVert^2\right]$
  - the larger the pruning error is, leading to a looser convergence bound



## Algorithm For Pruning Ratio Decision



## Evaluation



## Discussion