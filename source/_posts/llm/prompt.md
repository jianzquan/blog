---
title: Prompt-Tuning (LLM)
categories: LLM
tags: prompt
data: 2023-04-14
description: LLM 相关技术
---


## 1. 语言模型发展阶段
* **第一阶段**: Task-specific Fine-tuning
  
    ***过程***：对于具体任务，以预训练语言模型为backbone，引入额外参数适配任务，进行fine-tuning。
    
    ***问题***：① 下游任务目标与预训练目标差距过大；② 微调依赖大量监督语料

    ***代表***：BERT、GPT、XLNet

* **第二阶段**: Prompt-tuning
    
    ***过程***：逐步扩⼤模型参数和训练语料规模，探索不同类型的架构。

    ***代表***：BART、T5、GPT-3等；

* **第三阶段**: 
    
    ***过程***：⾛向AIGC（Artificial Intelligent Generated Content）时代，模型参数规模步⼊千万亿，模型架构为⾃回归架构，⼤模型⾛向对话式、⽣成式、多模态时代，更加注重与⼈类交互进⾏对⻬，实现可靠、安全、⽆毒的模型。

    ***代表***：InstructionGPT、Cha tGPT、Bard、GPT-4等。

<div align=center><img src="https://cdn.jsdelivr.net/gh/jianzquan/Rep4MyPage/img/LLM.jpg" width="800"></div>
<br/>


## 2. Prompt-Tuning
prompt-tuning 起源于GPT-3，GPT-3开创性地提出了in-context learning/demonstrate learning，由于其是建立在大规模预训练语言模型上的，参数量大于10B，在真实场景中很难应用。这套方法应用在小模型上，就是prompt-tuning了。

prompt-tuning 旨在解决传统fine-tuning的两个痛点问题：
* ***降低语义差异***：缩小pre-training与fine-tuning两个阶段目标差距。
* ***避免过拟合***：通过添加模板的方式避免引入额外的参数，进而造成的过拟合问题。
<br/>

Prompt-tuning 两个关键问题：（还有Ensembling的玩法）
* 模板构建(template): (大量优化方法)
  
  人工构建

  启发式发：PTR、AutoPrompt

  生成：LM-BFF、

  词向量微调

  伪标记：Prompt Tuning、P-tuning、Pre-trained Prompt Tuning、


* 标签词映射(label word verbilizer): KPT、ProtoVerb、

<div align=center><img src="https://cdn.jsdelivr.net/gh/jianzquan/Rep4MyPage/img/Prompt.jpg" width="800"></div>

<br/>

## 3. 面向LLM的Prompt-Tuning
研究发现，对于超过10亿参数量的模型来说。Prompt-tuning所带来的收益远远高于标准的Fine-tuning。

参数量够大、语料足够多、预训练任务足够有效，就能很好的实现免参数训练的零样本学习。

LLM的Prompt-tuning方法：
* **In-Context Learning**: (研究论文/技术很多很多)
    
    ***过程***：从训练集中挑选少量的标注样本，设计任务相关的指令形成提示模板，用于指导测试样本生成相应的结果。
    <div align=center><img src="https://cdn.jsdelivr.net/gh/jianzquan/Rep4MyPage/img/ICT.jpg" width="700"></div>
    
    ***问题***：如何选择样本？如何组合样本？(方差大、不稳定问题)

* **Instruction-tuning**:
  
    ***过程***：为各种任务定义指令，按指令模板重构输入进行训练。

* **Chain-of-Thought**: 进一步提高超大模型在复杂任务上的推理能力。
    
    ***过程***：代码的预训练




