---
layout: page
title: "Advancing Model Pruning via Bi-level Optimization"
description: "[NeurIPS22]"
img: assets/img/posts/bip_nips22/bip_overview.png
importance: 1
permalink: /projects/bip_nips22
github: "https://github.com/OPTML-Group/BiP"
category: EfficientML
---

#### Abstract

The deployment constraints in practical applications necessitate the pruning of large-scale deep learning models, i.e., promoting their weight sparsity. As illustrated by the Lottery Ticket Hypothesis (LTH), pruning also has the potential of improving their generalization ability. At the core of LTH, iterative magnitude pruning (IMP) is the predominant pruning method to successfully find ‘winning tickets’. Yet, the computation cost of IMP grows prohibitively as the targeted pruning ratio increases. To reduce the computation overhead, various efficient ‘one-shot’ pruning methods have been developed but these schemes are usually unable to find winning tickets as good as IMP. This raises the question of how to close the gap between pruning accuracy and pruning efficiency? To tackle it, we pursue the algorithmic advancement of model pruning. Specifically, we formulate the pruning problem from a fresh and novel viewpoint, bi-level optimization (BLO). We show that the BLO interpretation provides a technically-grounded optimization base for an efficient implementation of the pruning-retraining learning paradigm used in IMP. We also show that the proposed bi-level optimization-oriented pruning method (termed BIP) is a special class of BLO problems with a bi-linear problem structure. By leveraging such bi-linearity, we theoretically show that BIP can be solved as easily as first-order optimization, thus inheriting the computation efficiency. Through extensive experiments on both structured and unstructured pruning with 5 model architectures and 4 data sets, we demonstrate that BIP can find better winning tickets than IMP in most cases, and is computationally as efficient as the one-shot pruning schemes, demonstrating 2-7× speedup over IMP for the same level of model accuracy and sparsity. 

---

#### Model Pruning:

Model pruning is one of the mostly studied branch and has received increasing attention these years. Model pruning has demonstrated its effectiveness in many areas, such as reducing model size, improving model generalization, benefitting the model in terms of adversarial robustness, out-of-distribution generalization, transfer learning, etc. However, designing efficient and powerful pruning is still very challenging.


<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}/assets/img/posts/bip_nips22/efficient_ai.png" width="600">
    <br><br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999; font-size:18px；
    padding: 2px;">Figure 1. Model pruning is an important branch and research direction in promote efficient AI.</div>
    <br><br>
</center>


#### How to Find the Desired Sparse Model?


<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}/assets/img/posts/bip_nips22/imp.png" width="600">
    <br><br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999; font-size:18px；
    padding: 2px;">Figure 2. An illustration of the working pipeline of the iterative magnitude pruning (IMP).</div>
    <br><br>
</center>


<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}/assets/img/posts/bip_nips22/omp.png" width="600">
    <br><br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999; font-size:18px；
    padding: 2px;">Figure 3. An illustration of the working pipeline of the one-shot pruning methods.</div>
    <br><br>
</center>


#### Dillema in Model Pruning Methods: Effective Methods v.s. Efficient Methods? 



#### 

<center>
<b>
Is there an optimization basis for a successful pruning algorithm that can attain high pruned model accuracy (like IMP) and high computational efficiency (like one-shot pruning)?
</b>
</center>

As models usually learn "too well" during training - so much that make various types of attacks possible, backdoor attack (or Trojan Attack) has become a real-life threat to the AI model deployed in the real world. At the same time, extensive research work on model pruning has shown that the weights of an overparameterized model (e.g., DNN) can be pruned without hampering its generalization ability. Combining both lines of research, our story begins with the following question:


<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}/assets/img/publication_preview/sparse_trojan.png" width="600">
    <br><br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999; font-size:18px；
    padding: 2px;">Figure 1. An overview of our proposal: Weight pruning identifies the ‘winning Trojan ticket’, which can be used for Trojan detection and recovery.</div>
    <br><br>
</center>



#### Reference

<div id="refer-anchor-1"></div> 