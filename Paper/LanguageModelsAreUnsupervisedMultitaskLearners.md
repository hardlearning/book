# Language Models are Unsupervised Multitask Learners

## 2. Approach

Language modeling is usually framed as unsupervised distribution estimation from a set of examples $(x_1, x_2,\ldots, x_n)$ each composed of variable length sequences of symbols $(s_1, s_2,\ldots, s_n)$. Since language has a natural sequential ordering, it is common to factorize the joint probabilities over symbols as the product of conditional probabilities.

$$
p(x)=\prod_{i=1}^np(s_n|s_1,...,s_{n-1})
$$

This approach allows for tractable sampling from and estimation of p(x) as well as any conditionals of the form $p(s_{n-k},...,s_n|s_1,...,s_{n-k-1})$

Learning to perform a single task can be expressed in a probabilistic framework as estimating a conditional distribution $p(output|input)$. Since a general system should be able to perform many different tasks, even for the same input, it should condition not only on the input but also on the task to be performed. That is, it should model $p(output|input, task)$. This has been variously formalized in multitask and meta-learning settings.

Language provides a flexible way to specify tasks, inputs, and outputs all as a sequence of symbols. For example, a translation training example can be written as the sequence (translate to french, english text, french text). Likewise, a reading comprehension training example can be written as (answer the question, document, question, answer).

Language modeling is also able to learn the tasks without the need for explicit supervision of which symbols are the outputs to be predicted. Since the supervised objective is the the same as the unsupervised objective but only evaluated on a subset of the sequence, the global minimum of the unsupervised objective is also the global minimum of the supervised objective.

The problem instead becomes whether we are able to, in practice, optimize the unsupervised objective to convergence.

Preliminary experiments confirmed that sufficiently large language models are able to perform multitask learning in this toy-ish setup but learning is much slower than in explicitly supervised approaches.

### 2.1. Training Dataset

Instead, we created a new web scrape which emphasizes document quality. To do this we only scraped web pages which have been curated/filtered by humans.

Manually filtering a full web scrape would be exceptionally expensive so as a starting point, we scraped all outbound links from Reddit, a social media platform, which received at least 3 karma. This can be thought of as a heuristic indicator for whether other users found the link interesting, educational, or just funny.

We removed all Wikipedia documents from WebText since it is a common data source for other datasets and could complicate analysis due to overlapping training data with test evaluation tasks.

### 2.2. Input Representation

A general language model (LM) should be able to compute the probability of (and also generate) any string. Current large scale LMs include pre-processing steps such as lowercasing, tokenization, and out-of-vocabulary tokens which restrict the space of modelable strings.

Byte Pair Encoding (BPE) is a practical middle ground between character and word level language modeling which effectively interpolates between word level inputs for frequent symbol sequences and character level inputs for infrequent symbol sequences.

Despite its name, reference BPE implementations often operate on Unicode code points and not byte sequences. These implementations would require including the full space of Unicode symbols in order to model all Unicode strings.

However, directly applying BPE to the byte sequence results in sub-optimal merges due to BPE using a greedy frequency based heuristic for building the token vocabulary.

We observed BPE including many versions of common words like dog since they occur in many variations such as dog. dog! dog? . This results in a sub-optimal allocation of limited vocabulary slots and model capacity.

To avoid this, we prevent BPE from merging across character categories for any byte sequence. We add an exception for spaces which significantly improves the compression efficiency while adding only minimal fragmentation of words across multiple vocab tokens.

This input representation allows us to combine the empirical benefits of word-level LMs with the generality of byte-level approaches. Since our approach can assign a probability to any Unicode string, this allows us to evaluate our LMs on any dataset regardless of pre-processing, tokenization, or vocab size.

#### Vacabulary

- be framed as 被视为
- unsupervised distribution estimation 无监督分布估计
- compose of 由......组成
- factorize ... as 将...的因子化为
- tractable sampling 可控的抽样
- expressiveness of models 模型的表现力
- probabilistic framework 概率框架
- condition ... on 以...为条件
- formalized 公式化
- multitask 多任务
- meta-learning 元学习
- exemplify 举例
- explicit 明确的
- toy setting 较小的设置
- the concerns are side stepped. 问题迎刃而解
- density estimation 密度测定
- preliminary experiments 初步试验
- toy-ish 玩具式的
- well-posed setup 适定的设置
- messiness 混乱
- in the context of 在...的背景下
- for the need to do sth 有必要做某事
- capable of 能够
- reward signal 奖励信号
- forward prediction 前瞻性预测
- be passively available 被动获取
- speculation 推测
- demonstrate 演示
- procurement 采购
- zero-shot setting 零样本设置
- promising 有潜力的，有前途的
- archives 档案
- unintelligible 难以理解的
- pragmatic approach 实用的方法
- curate 策划
- outbound links 外链
- karma 因果报应
- heuristic indicator 启发式指标
- de-duplication 去重复
- the space of modelable strings 可建模字符的空间
- performance gap 性能差距
- interpolate 插入
- frequent symbol sequences 频繁出现的符号序列
- multi-symbol tokens 多符号标记
- prohibitively 过分地
- sub-optimal merges 次优合并
- greedy frequency 贪婪频率
- sub-optimal allocation 次优分配
- vocabulary slots 词汇槽
- merging across character categories 跨字符类别合并
- add an exception 添加一个例外
- compression efficiency 压缩效率
- minimal fragmentation of words 极少的单词碎片
- empirical benefits 经验优势
- generality 通用性
- regardless of 无需考虑
