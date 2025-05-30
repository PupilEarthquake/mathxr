---
title: "形式化数学推理"
date: 2025-05-07
# bookComments: false
# bookSearchExclude: false
linktitle: 形式化数学推理
menu: main
weight: 1
categories: "Read"
tags: ["CS", "Type Theory"]
---

# Introduction
AI实现数学推理可视作两条路径: 一是非形式化推理, 如大语言模型(LLM); 二是形式化推理, 如编程语言Lean. _Formal Mathmatical Reasonling: A New Frontier in AI_ (下面简称文章)总结了这些领域现有的进展; 讨论了公开的挑战; 并且展望了未来里程碑式突破的衡量标准. 此博客简单复述了论文中关于近期进展的内容, 并抛出了一些读者的看法.

# Two Lines: Informal / Formal Mathematics
非形式化方法指搭建数学大语言模型来解决问题, 就像问Deepseek R1数学问题那样. 常见的做法是在数学教材, 数学论文等文本上训练LLMs. LLM的优点在于灵活性, 可以处理自然语言.

所谓形式数学推理是指在形式系统下表达数学. 一个形式系统具有 well-formed 的语法, 并且可以通过一组 well-defined 的规则进行推理. 比如公理集合论, 高阶逻辑(higher-order logic), 依赖类型论(dependent type theory). 几乎所有的数学都可以用ZFC公理系统下一阶逻辑来表达, 而这正是通常的研究生数学教材开篇所做的事情. 数学也可以在依赖类型论下表达, Lean便是如此. 相比于非形式化方法, 形式系统保证了推理过程100%正确, 并且可以提供反馈, 比如在使用Lean时软件会显示每一步推理后目标是否达成. 

我们已经见识过, LLM在思考数学问题时难免会出现一本正经地胡说八道的情况; 同时非形式化方法还面临高质量数学文本缺乏的难题. 这是非形式化的缺点. 另一方面, 形式化方法也有明显缺点. Lean早在2013年就由微软研究院推出, 在这之前还有Coq, Isabelle等项目. 虽然获得了少量数学家的注意, 并且也有数学家在极力推广(如Kevin Buzzard), 但至今没有被大众接受. 结合个人使用体验, 我认为原因至少有三点:

- 将自然语言文本翻译成形式语言麻烦且耗时.
- 形式化后的数学就像是程序代码, 可读性极差.
- 不同证明器可能采用了不同的底层逻辑. 就Lean来说, 学习依赖类型论依然需要成本, 学习编程语法也需要成本.

因此未来的发展会在两条技术路径的交叉地带. 文章作者相信: __基于AI的形式数学推理已经来到了转折点.__

# Recent Progress

## Autoformalization

自动形式化就是将自然语言数学文本翻译成形式化数学文本. 常见的方法有两个:

__Rule Based Autoformalization:__ 为了应对自然语言的灵活性和复杂性, 消除单词和符号的歧义, 许多系统采用了受控自然语言(controlled natural language)来支持用户以又自然又形式化的方法来表达数学. 这种语言是自然语言的子集, 具有形式化的语法. 

__Neural and LLM-based Autoformalization:__ 早期的这方面实验使用机器学习将自然语言翻译成形式语言, 但这种方法严重依赖于非形式化和形式化语句的对齐语料库. 如今的LMM也可在一定程度上进行这类翻译任务, 但依然存在翻译不准确的问题.

## Neural Theorem Proving

文章将形式系统下的数学推理和桌游(围棋, 国际象棋等)作类比. 推理的进行必须合法, 这就好比棋子在棋盘走动. 而下棋AI已经展示了它们的力量. 

任何有足够表达力的形式化系统中, 定理证明都是不可判定的, 因此需要使用启发式算法. 常见的有这几类:

__Expert Iteration:__ 每当模型找到新的证明后, 都可以将其作为新的训练数据. 但收益往往会在几次迭代后减少.

__Learning from Mistakes:__ 形式化证明环境可以在某一步骤证明失败时提供错误消息, 利用这一特性可以辅助LLM的学习, 降低犯同一类错误的几率. 但如何识别和学习这些错误还是一项挑战.

__Informal Proof Sketches:__ 使用LMM以自然语言生成证明草图, 再将这些草图形式化. 

__Library Learning:__ 利用一个不断增长的数学结果库来寻找新的结果. 除了寻找证明外, 也可以缩短现有的证明路线.

__Premised Selection and Retrival:__ 这是一种拥有大型数学结果库时的方案. 一个例子是Retrieval-augumented Generation(RAG), 其在尝试生成证明之前, 先从数据库中检索可能有用的数据, 再将这些数据提供给LLM, 检索可能用于证明目标定理的引理.

## Verified Reasoning in Natural Language

在自然语言的验证推理方面, 目前也有两个常见手段. 

其一是通过训练有素的验证器, 少量提示(few-shot prompted)的验证器, 或符号验证器(symbolic verifier)来验证自然语言推理. 这类方法无法保证推理的合法性, 只能提高忠实度.

其二是使用LLM将自然语言形式化, 再用符号求解器(symbolic solver)寻找答案. 这种方法同样面临挑战: 难以互相翻译自然语言和形式语言, 也无法保证问题被正确形式化.

## Formal System Verification and Verified Generation

软件和硬件系统的形式化验证是形式数学最重要的应用之一, 人们首先将系统的正确性和安全性要求声明为形式化断言(formal assertions), 再使用定理证明器和模型检查技术来证明系统满足要求, 或以此来排查错误.

Deductive theorem proving 已被应用在许多关键系统中, 如操作系统内核, 文件系统等. 但编写形式化规范和证明总是凝聚了大量的劳动力. 而神经定理证明可以应用于这些系统验证工作, LLM也可助力于生成断言以及翻译自然语言的工作.

这里文章中还写了一些非常有价值的挑战, 多是关于代码或程序设计的, 我实在看不懂, 只感觉一股流浪地球的味道扑面而来. 各位如果感兴趣请移步原文. 文章后面主要讨论了这些内容:

- 公开的挑战. 比如形式化数学文本缺乏的问题.
- 里程碑和成功标准. 作者将定理证明, 自然语言验证等方面的发展分成了几个等级.



# My View

以下观点带有强烈的主观成分, 是我近期见闻的感受, 读者大可绕过. 

这篇博客发表前数天, 我首次接触到形式系统还有类型论(Type Theory)等等技术. 这些东西给了我巨大的震撼, 有段时间我也非常担忧自己的未来.

<!--
数学是一个诞生于人类自然语言的事物, 数学的运转依赖于符号学系统本身的运转. 似乎很多人认为数学符号脱离于自然语言, 还认为公式反映了宇宙的本质. 其实不然. 所有的数学符号都可完全展开为自然语言来描述, 为了感觉到这一点, 不妨从头开始翻阅一本数学书, 然后去解释书中出现的任何符号. 数学公式和现实有对应, 并不是数学描述了宇宙的本质, 而是你我口中的宇宙也是被自然语言构建起来的. 语言, 构成了我们理性认识的全部. 数学是自然语言的子集, 数学的有效来源于明确的推理规则.

我从很久前就开始思考, 有没有可能能将数学全部规范化, 数字化, 让其能像程序一样运行. 比如当我给定了所需公理, 程序能自动根据我给出的条件, 计算出所有可行的结果. 直到我遇到Lean, 形式化数学, 我发现这已经非常接近我的幻想. 不过现有的技术无法实现略微复杂的自动证明. 有一个瞬间我觉得自己看到了数学的未来, 于是才开始搜索相关论文, 最后产生了这篇博客.
-->

用纸笔人脑进行推理可能过于原始, 人类不可能在数千年后还在维持现在的研究方式. 因此我觉得数学推理的数字化是历史的潮流, 只不过它的未来不一定会是Lean, 或许会是别的更好读写的语言. 

另外, 关于纯数学工作者是否会失业, 我觉得短期内不会, 但到了近未来对纯数学工作者的需求量会变少, 理由是:

- 如上文所述, 短期内技术能触及的极限就是自动形式化和自动证明. 但idea的发现, 新数学的发明依然需要人类来完成. 
- 必须得有人了解实现形式化数学的技术, 才能持续维护和更新这一技术.
- 可靠的自动证明技术的出现, 必然会引起AI技术的爆炸, 到那时受影响的可不只数学行业.

接下来, 我可能会花时间了解一下类型论. 论文中写道, 2023年到2024年间, 有关形式数学推理的论文数量几乎翻了一倍. 我有一种感觉, 我们正处在某个巨大变革的前夕.



# Useful Links
1. Formal Mathmatical Reasonling A New Frontier in AI: https://arxiv.org/abs/2412.16075
2. 计算机辅助证明介绍: https://zhuanlan.zhihu.com/p/181671237
3. Lean技术介绍: https://lean-lang.org/papers/system.pdf
4. Kevin Buzzard的博客: https://xenaproject.wordpress.com/useful-links/
