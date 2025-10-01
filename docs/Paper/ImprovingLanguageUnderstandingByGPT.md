# Improving Language Understanding by Generative Pre-Training

## 3 Framework

Our training procedure consists of two stages. The first stage is learning a high-capacity language model on a large corpus of text. This is followed by a fine-tuning stage, where we adapt the model to a discriminative task with labeled data.

### 3.1 Unsupervised pre-training

Given an unsupervised corpus of tokens $\mathcal{U}=\{u_1,\ldots,u_n\}$, we use a standard language modeling objective to maximize the following likelihood:

$$
L_1(\mathcal{U})=\sum_i\log P(u_i|u_{i-k},\ldots,u_{i-1};\Theta)
$$

where k is the size of the context window, and the conditional probability P is modeled using a neural network with parameters $\Theta$. These parameters are trained using stochastic gradient descent.

In our experiments, we use a multi-layer *Transformer decoder* for the language model. This model applies a multi-headed self-attention operation over the input context tokens followed by position-wise feedforward layers to produce an output distribution over target tokens:

$$
\begin{aligned}
h_{0}& =UW_{e}+W_{p} \\
h_{l}& =\text{transformer \_block}(h_{l-1})\forall i\in[1,n] \\
P(u)& =\text{softmax}(h_nW_e^T) 
\end{aligned}
$$

where $\mathcal{U}=(u_{−k},\ldots,u_{−1})$ is the context vector of tokens, n is the number of layers, $W_e$ is the token embedding matrix, and $W_p$ is the position embedding matrix.

### 3.2 Supervised fine-tuning

We assume a labeled dataset $\mathcal{C}$, where each instance consists of a sequence of input tokens, $x^1,\ldots,x^m$, along with a label y. The inputs are passed through our pre-trained model to obtain the final transformer block’s activation $h_l^m$, which is then fed into an added linear output layer with parameters $W_y$ to predict y:

$$
P(y|x^1,\ldots,x^m)=\text{softmax}(h_l^mW_y)
$$

This gives us the following objective to maximize:

$$
L_2(\mathcal{C})=\sum\limits_{(x,y)}\log P(y|x^1,\ldots,x^m)
$$

We additionally found that including language modeling as an auxiliary objective to the fine-tuning helped learning by (a) improving generalization of the supervised model, and (b) accelerating convergence.

Specifically, we optimize the following objective (with weight $\lambda$):

$$
L_3(\mathcal{C})=L_2(\mathcal{C})+\lambda*L_1(\mathcal{C})
$$

Overall, the only extra parameters we require during fine-tuning are $W_y$, and embeddings for delimiter tokens.

### 3.3 Task-specific input transformations

For some tasks, like text classification, we can directly fine-tune our model as described above. Certain other tasks, like question answering or textual entailment, have structured inputs such as ordered sentence pairs, or triplets of document, question, and answers. Since our pre-trained model was trained on contiguous sequences of text, we require some modifications to apply it to these tasks.

Previous work proposed learning task specific architectures on top of transferred representations. Such an approach re-introduces a significant amount of task-specific customization and does not use transfer learning for these additional architectural components. Instead, we use a traversal-style approach, where we convert structured inputs into an ordered sequence that our pre-trained model can process.

These input transformations allow us to avoid making extensive changes to the
architecture across tasks. We provide a brief description of these input transformations below and Figure 1 provides a visual illustration. All transformations include adding randomly initialized start and end tokens (\<s\>, \<e\>).

Figure 1: (left) Transformer architecture and training objectives used in this work. (right) Input transformations for fine-tuning on different tasks. We convert all structured inputs into token sequences to be processed by our pre-trained model, followed by a linear+softmax layer.

- Textual entailment: For entailment tasks, we concatenate the premise p and hypothesis h token sequences, with a delimiter token ($) in between.
- Similarity: For similarity tasks, there is no inherent ordering of the two sentences being compared. To reflect this, we modify the input sequence to contain both possible sentence orderings (with a delimiter in between) and process each independently to produce two sequence representations $h_l^m$ which are added element-wise before being fed into the linear output layer.
- Question Answering and Commonsense Reasoning: For these tasks, we are given a context document $z$, a question $q$, and a set of possible answers $\{a_k\}$. We concatenate the document context and question with each possible answer, adding a delimiter token in between to get $[z;q;\$;a_k]$. Each of these sequences are processed independently with our model and then normalized via a softmax layer to produce an output distribution over possible answers.

#### Vacabulary

- high-capacity language model: 高容量语言模型
- fine-tuning: 微调
- adapt: 调整，使适应
- discriminative task: 判别任务
- standard language modeling objective: 标准语言建模目标
- be modeled: 建模
- position-wise feedforward layers: 位置前馈层
- auxiliary objective: 辅助目标
- convergence: 收敛
- delimiter: 分隔符
- textual entailment: 文本蕴含
- triplet: 三元组
- transferred representations: 转移表征
- task-specific customization: 特定任务的定制
- architectural components: 架构组件
- traversal-style: 遍历式的
- premise: 前提
- inherent: 固有的
- Commonsense Reasoning: 常识推理
- be added element-wise: 按元素相加
