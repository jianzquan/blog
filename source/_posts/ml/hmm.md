---
title: HMM
categories: ML
tags: hmm
sticky: 1
cover: ./img/cartoon_1.jpg
copyright: false
---

## Hidden Markov Model
### 符号
* 观测序列: $X=\{ x_{1}, ..., x_{T} \}$ (离散/连续取值均可)
* 隐藏序列: $Z=\{ z_{1}, ..., z_{T} \}$ (每个$z_{i}$有N种离散取值)
* 模型参数: $\lambda=(\pi, A, B)$
### 基本假设
* 齐次Markov假设: (t+1时刻 隐藏状态只与前一时刻隐藏状态相关) 
  
  $p(z_{t+1}|z_{t},...,z_{1},x_{t},...,x_{1})=p(z_{t+1}|z_{t})$

* 观测独立假设: (t时刻 观测状态只与 t时刻 隐藏状态相关)
  
  $p(x_{t}|z_{t},...,z_{1},x_{t-1},...,x_{1})=p(x_{t}|z_{t})$

### 三个问题
* Evaluation: (已知模型参数, 求概率最大的观测序列 $X$) 
  
  $p(X|\lambda)$ $\to$ Forward-Backward 算法

* Learning: (已知观测序列, 求模型参数)
  
  $\lambda=argmax_{\lambda} \ p(X|\lambda)$ $\to$ EM 算法 

* Decoding: (已知模型参数和观测序列, 求概率最大的隐藏序列)
  
  $Z=argmax_{Z} \ p(Z|X, \lambda)$ $\to$ Vierbi 算法
    
    1) Filter: $p(z_{t}|x_{1},...,x_{t})$
    2) Predict: $p(z_{t+1}|x_{1},...,x_{t})$

<div align=center><img src="https://cdn.jsdelivr.net/gh/jianzquan/Rep4MyPage/img/HMM.png" width="600"></div>
<br/>

### Forward Algorithm
$\alpha_{t}(i)=p(x_{1},...,x_{t}, z_{t}=q_{i}|\lambda)$ (t时刻, 给定前t个观测状态,隐藏状态为 $q_{i}$ 的概率)

$\alpha_{t+1}(j)=\sum_{i=1}^{N}b_{j}(x_{t})a_{ij} * \alpha_{t}(i)$

### Backward Algorithm
$\beta_{t}(i)=p(x_{t+1},...,x_{T}|z_{t}=q_{i}, \lambda)$ (t时刻, 给定后续观测状态, 隐藏状态为 $q_{i}$ 的概率)

$\beta_{t}(i)=\sum_{j=1}^{N}b_{j}(x_{t+1})a_{ij} * \beta_{t+1}(j)$


### Tasks
#### Learning
* $\lambda=argmax_{\lambda} \ p(X|\lambda)$
    
    $p(X|\lambda)=\sum_{Z}p(Z,X|\lambda)=\sum_{Z}p(X|Z,\lambda)p(Z|\lambda)$
#### Inference
* Decoding: 
  
  $Z=argmax_{Z} \ p(Z|X, \lambda)$
  
* Prob of evidence: 
  
  $p(X)$

* Filtering: 
  
  $p(z_{t}|x_{1},...,x_{t})$
* Smoothing: 
  
  $p(z_{t}|x_{1},...,x_{T})$
* Prediction: 

   $\left\{ 
     \begin{array}{l}
       p(z_{t+1}|x_{1},...,x_{t}) \\
       p(x_{t+1}|x_{1},...,x_{t})
     \end{array}
  \right.$
  
<!-- $$ \left\{
  \begin{array}{l}
    Learning: \lambda=argmax_{\lambda} \ p(X|\lambda) \\
    Inference 
      \left\{
        \begin{array}{l}
          Decoding: Z=argmax_{Z} \ p(Z|X, \lambda) \\
          Prob \ of \ evidence: p(X) \\
          Filtering: p(z_{t}|x_{1},...,x_{t}) \\
          Smoothing: p(z_{t}|x_{1},...,x_{T}) \\
          Prediction:
             \left\{ 
               \begin{array}{l}
                 p(z_{t+1}|x_{1},...,x_{t}) \\
                 p(x_{t+1}|x_{1},...,x_{t})
               \end{array}
            \right.
        \end{array}
      \right.
  \end{array}
\right. $$ -->
