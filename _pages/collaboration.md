---
layout: research
title: Research
permalink: /research/
description:
nav: false
nav_order: 2
---

# Research Statement

As artificial intelligence (AI) systems move from the laboratory into the real world, a paramount requirement is to develop algorithms that are robust, fair, and interpretable prior to deployment. Moreover, only scalable ML algorithms can better apply to the increasingly complex datasets, models, and tasks. Thus, my research focuses on the **trustworthy** and **scalable** ML algorithms. In general my research scope spans the areas of machine learning (ML)/deep learning (DL), optimization theory, computer vision, and security. These research topics provide a solid foundation for my current and future research: *Making AI system safe and scalable.* My research on these two goals are intervened and can be summarized as the following two perspectives:

:heavy_check_mark: **Algorithmic perspective**: This line of research designs the scalable and theoretically-grounded machine learning algorithms subject to real-life constraints, e.g., computation/communication overhead, robustness, fairness, and interpretability.

:heavy_check_mark: **Application perspective**: This line of research tackles the domain-specific challenges to achieve scalable and trustworthy AI, e.g., robustness enhancement, fairness promotion, data privacy protection, and model compression.

{% include figure.html path="assets/img/research.png" class="img-fluid rounded z-depth-1" zoomable=true %}
<div class="caption">
  An overview of my research.
</div>

#### Scalable Bi-level Optimization: Theory and Application

Bi-level optimization (BLO) has been emerged as a technology basis in solving many recent machine learning (ML) problems, such as attack and defense design in adversarial ML, meta learning, hyper-parameter optimization, and model pruning. My work focuses on reformulating existing ML problems and advancing their algorithmic foundations through theoretically-grounded, empirically outstanding and scalable BLO algorithms \[[2](#refer-anchor-2), [4](#refer-anchor-4), [8](#refer-anchor-8)\].

**Scalable BLO algorithm and theory**

Compared to the conventional min-max problems, BLO offers us a unified hierarchical learning framework, where one task is nested inside the other (i.e., the objective and variables of an upper-level problem depend on the optimizer of the lower-level problem). Such a structure makes the BLO in its most generic form very difficult to solve and the hard to scale. Thus, I ask: 

> How to build theoretically-grounded BLO framework for ML problems with light computational complexity?

My work \[[2](#refer-anchor-2)\] proposed the first scalable BLO algorithm for robust training and my work \[[4](#refer-anchor-4)\] also proposed a purely first-order BLO algorithm for model pruning, which achieves the best performance with much higher efficiency compared to the state-of-the-art baseline. 


#### Trustworthy AI: Robustness, Fairness, and Explanability

As researchers realize that solely high accuracy is not enough to make AI systems safe, responsible and worthy of the trust, the urge to build a *robust, fair, explainable* AI system has been described by some experts as the biggest challenges of the next 5 years \[[9](#refer-anchor-9)\]. Thus, a large part of my work is dedicated to promote the robustness, fairness, and transparency of the AI system.

* Robustness: Adversarial training (AT) is one of the most famous methods to equip models with robustness, while it is also known for its intensive computational cost. To enable AT to support large datasets and model architectures, my work \[[1](#refer-anchor-1)\] provides the first distributed robust training framework that scale up various robust training algorithms, including AT, certified training, and robust unsupervised training, which won the Best Paper Runner-up Award in UAI'22. Single-step AT is also an important branch of algorithms that serve to accelerate AT. Accordingly, my work \[[2](#refer-anchor-2)\] advances the optimization foundation of accelerated AT through BLO and provides a promising solution with an attack-agnostic robust training framework. In the area of NLP, my work \[[6](#refer-anchor-6)\] also proposed the first gradient-driven attack generator for language models, which successfully overcame the discrete nature of the textual input and the additional constraint of the perturbation. With the help of the newly designed attack, \[[6](#refer-anchor-6)\] promoted the adversarial defense of NLP tasks to the next level.

* Fairness: My fairness reprogramming work \[[5](#refer-anchor-5)\] achieved to promote the fairness of the models without changing the model weights in both NLP and CV tasks. I also achieved in reducing the model biases in the black-box setting, where only the outputs of the model API are accessible. 

* Explanability: Trojan attack has also arisen as a real-world threaten to various ML systems. My work \[[3](#refer-anchor-3)\] reveals why the backdoor works from the perspective of model compression and further proposes an effective data-free backdoor detection method.

<center>
{% include figure.html path="assets/img/bip.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
</center>
<div class="caption">
  Bi-level optimization advances the algorithmic foundation of model pruning.
</div>

#### Sparse Learning for Model Compression

Model sparsity has seen a lot of research interests these years, as reducing model size by removing redundant parameters has been known to benefit model generalization, adversarial robustness, out-of-distribution generalization, and transfer learning. My work \[[4](#refer-anchor-4)\] reformulated the model pruning problem as a bi-level optimization problem, and proposed a theoretically-grounded algorithm, which achieves the new state-of-the-art performance and provides a whole new perspective for model pruning to the community. Sparsity can also help interpret backdoor attacks, as my work \[[3](#refer-anchor-3)\] reveals that model pruning is more likely to remove the benign features compared to the backdoor features. Accordingly, I designed a clean data-free backdoor detection method leveraging model sparsity.

---

#### Reference

<div id="refer-anchor-1"></div> [1] G. Zhang\*, S. Lu\*, <b>Y. Zhang</b>, X. Chen, P. Chen, Q. Fan, L. Martie, M. Hong, S. Liu, “Distributed Adversarial Training to Robustify Deep Neural Networks at Scale”, Conference on Uncertainty in Artificial Intelligence (UAI’22 - Best Paper Runner-up Award)

<div id="refer-anchor-2"></div> [2] <b>Y. Zhang</b>*, G. Zhang*, P. Khanduri, M. Hong, S. Chang, S. Liu, “Fast-BAT: Revisiting and Advancing Fast Adversarial Training through the Lens of Bi-level Optimization”, International Conference on Machine Learning (ICML’22)

<div id="refer-anchor-3"></div> [3] T. Chen\*, Z. Zhang\*, <b>Y. Zhang</b>\*, Chang, S. Liu, W. Yang, “Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free”, Computer Vision and Pattern Recognition Conference (CVPR’22)
<div id="refer-anchor-4"></div> [4] <b>Y. Zhang</b>\*, Y. Yao\*, P. Ram, P. Zhao, T. Chen, M. Hong, Y. Wang, S. Liu, “Advancing Model Pruning via Bi-level Optimization” (NeurIPS'22)

<div id="refer-anchor-5"></div> [5]G. Zhang\*, <b>Y. Zhang</b>\*, Z. Zhang, W. Fan, Q. Li, S. Liu, S. Chang, “Fairness Reprogramming” (NeurIPS'22)

<div id="refer-anchor-6"></div> [6 B. Hou, J. Jia, <b>Y. Zhang</b>, G. Zhang, Y. Zhang, S. Liu, S. Chang, "TextGrad: Advancing Robustness Evaluation in NLP by Gradient-Driven Optimization" (ICLR'23)

<div id="refer-anchor-7"></div> [7] H. Li, S. Zhang, M. Wang, <b>Y. Zhang</b>, P. Chen, S. Liu, "Theoretical Characterization of Neural Network Generalization with Group Imbalance" (under review)

<div id="refer-anchor-8"></div> [8] P. Khanduri, I. Tsaknakis, <b>Y. Zhang</b>, J. Liu, S. Liu, J. Zhang, M. Hong, "Linearly Constrained Bilevel Optimization: A Smoothed Implicit Gradient Approach" (under review)

<div id="refer-anchor-9"></div> [9] <b>Y. Zhang</b>, P. Sharma, P. Ram, M. Hong, K. R. Varshney, S. Liu, "What Is Missing in IRM Training and Evaluation? Challenges and Solutions " (ICLR'23)




