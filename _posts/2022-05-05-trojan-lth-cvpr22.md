---
layout: paper
title:  "[CVPR22] Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free"
date: 2022-06-21 21:00:00
author: "<a style='color: #dfebf7' href='https://tianlong-chen.github.io/'>Tianlong Chen</a><sup>[1]</sup>*, 
         <a style='color: #dfebf7' href='https://scholar.google.com/citations?user=ZLyJRxoAAAAJ&hl=zh-CN'>Zhenyu Zhang</a><sup>[1]</sup>*, 
         <a style='color: #dfebf7' href='https://www.yihua-zhang.com/'>Yihua Zhang</a><sup>[2]</sup>*, 
         <a style='color: #dfebf7' href='https://code-terminator.github.io/'>Shiyu Chang</a><sup>[3]</sup>, 
         <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[2,4]</sup>, 
         <a style='color: #dfebf7' href='https://vita-group.github.io/'>Zhangyang Wang</a><sup>[1]</sup>"
affiliation: "<sup>[1]</sup>University of Texas at Austin, <sup>[2]</sup>Michigan State University, <sup>[3]</sup>University of California, Santa Barbara, <sup>[4]</sup>MIT-IBM Watson AI Lab"
code: "https://github.com/VITA-Group/Backdoor-LTH"
poster: "https://www.yihua-zhang.com/assets/posters/trojan_lth.pdf"
paper: "https://github.com/VITA-Group/Backdoor-LTH"
tags: "TrustworthyML"
categories: "cvpr22"
---

#### Motivation

As models usually learn "too well" during training - so much that make various types of attacks possible, backdoor attack (or Trojan Attack) has become a real-life threat to the AI model deployed in the real world. At the same time, extensive research work on model pruning has shown that the weights of an overparameterized model (e.g., DNN) can be pruned without hampering its generalization ability. Combining both lines of research, our story begins with the following question:

<center>
<b>

How does the model sparsity relate to its train-time robustness against Trojan attacks?
</b>
<br>
</center>

---

#### The Discovery of 'Winning Trojan Ticket'

We start our research by making an observation on the performance change of a backdoored model as we gradually increase the model sparsity with the model pruning technique. More specifically, we would like to see how the clean accuracy (CA) as well as attack success rate (ASR) will change with respect to the increasing sparsity. We plot the curve of CA and ASR w.r.t. sparsity ratio in Figure 1. Some interesting phenomena we listed below indicate that there is a strong connection between model sparsity and Trojan features.

As ASR is constantly higher than CA, and CA drops much faster than ASR, Trojan features learned by backdoored attacks are significantly more stable against pruning than benign features. Therefore, we assume that "Trojan attacks can be uncovered through the pruning dynamics of the Trojan model". The question remains: how to leverage the 'stubbornness' of the Trojan features to detect the Trojan attack itself?

As we further increase the model sparsity, both ASR and CA reasonably fall to a relatively low level. However, at a certain sparsity level, the ASR surges to a conspicuously high level while the CA remains low, which we term the 'winning Trojan Ticket', borrowing the idea from LTH-oriented [\[1\]](#refer-anchor-1) iterative magnitude pruning. The performance of the winning Trojan Ticket implies that such a model subnetwork preserves the Trojan attack traces while retaining chance-level performance on clean inputs. In other words, it is a 'purely bad' subnetwork.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/backdoor_cvpr22/overview.png" title="example image" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 1. An overview of our proposal: Trojan features learned by backdoored attacks are significantly more stable against pruning than benign features. Therefore, Trojan attacks can be uncovered through the pruning dynamics of the Trojan model. Weight pruning identifies the ‘winning Trojan ticket’, which can be used for Trojan detection and recovery. 
</div>

Leveraging LTH-oriented iterative magnitude pruning (IMP), the ‘winning Trojan Ticket’ can be discovered, which preserves the Trojan attack performance while retaining chance-level performance on clean inputs.

Thus, the existence of the 'winning Trojan Ticket' could serve as an indicator of Trojan attacks. However, in real-world applications, it is hard for the users to acquire the ASR (namely the red curve in Figure 1), as the attack information is transparent to the users. Thus, we need to find a substitute indicator for ASR, which does not require any attack information or even clean data.

The winning Trojan ticket can be detected by our proposed linear model connectivity (LMC)-based Trojan score.

---

#### Trojan Score: Linear Mode Connectivity-based Trojan Indicator

We adopt Linear Mode Connectivity [\[2\]](#refer-anchor-2) (LMC) to measure the stability of the Trojan ticket $$\phi := (m \odot \theta)$$ v.s. the $$k$$-step finetuned Trojan ticket $$\phi := (m \odot \theta^{(k)})$$.

We define the Trojan Score as

$$
    \mathcal{S}_{Trojan} = \max_{\alpha \in [0, 1]} \mathcal{E} (\alpha \phi - (1 - \alpha)\phi_{k}) - \frac{\mathcal{\phi} - \mathcal{\phi_k}}{2}
$$

where the first term denotes LMC and the second term an error baseline. $$\mathcal{E}(\phi)$$ denotes the training error of the model $$\phi$$.

A sparse network with the peak Trojan Score maintains the highest ASR in the extreme pruning regime and is termed as the Winning Trojan Ticket.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/backdoor_cvpr22/pruning_dynamic.png" title="example image" class="img-fluid rounded z-depth-1" zoomable=true%}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 2. The pruning dynamics of Trojan ticket (dash line) and 10-step finetuned ticket (solid line) on CIFAR-10 with ResNet-20 and gray-scale backdoor trigger. For comparison, the Trojan score is also reported.
</div>

---

#### Trojan Trigger Reverse Engineer 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/backdoor_cvpr22/trigger_l1_norm.png" title="example image" class="img-fluid rounded z-depth-1" zoomable=true%}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 3. The \(\ell_1\) norm values of recovered Trojan triggers for all labels. The plot title signifies network architecture, trigger type, and the images for reverse engineering on CIFAR-10. Class “1” is the true target label for Trojan attacks. Green check or red cross indicates whether the detected label (with the least \(\ell_1\) norm matches the true target label).
</div>

---

#### Trigger Reverse Engineer

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/backdoor_cvpr22/recover_trigger_poster.png" title="example image" class="img-fluid rounded z-depth-1" zoomable=true%}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 4. Visualization of recovered Trojan trigger patterns from dense Trojan models (baseline) and winning Trojan tickets. ResNet-20s on CIFAR-10 with RGB triggers are used. The first column shows the random seed images used for trigger recovery.
</div>

---

#### Citation

```
@inproceedings{chen2022quarantine,
  title = {Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free},
  author = {Chen, Tianlong and Zhang, Zhenyu and Zhang, Yihua and Chang, Shiyu and Liu, Sijia and Wang, Zhangyang},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages = {598--609},
  year = {2022}
}
```
---

#### Reference

<div id="refer-anchor-1"></div> [1] Jonathan Frankle et al. “The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks.” ICLR 2019. 

<div id="refer-anchor-2"></div> [2] Jonathan Frankle et al. “Linear Mode Connectivity and the Lottery Ticket Hypothesis.” ICML 2020.

<div id="refer-anchor-3"></div> [3] Ren Wang et al. “Practical detection of trojan neural networks: Data-limited and data-free cases.” ECCV 2020.