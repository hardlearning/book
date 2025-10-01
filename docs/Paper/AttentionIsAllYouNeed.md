# Attention Is All You Need

DOI: https://doi.org/10.48550/arXiv.1706.03762

## 3 Model Architecture

Most competitive neural sequence transduction models have an encoder-decoder structure.

Here, the encoder maps an input sequence of symbol representations $(x_1,\ldots ,x_n)$ to a sequence of continuous representations $\mathbf{z}=(z_1,\ldots ,z_n)$. Given $\mathbf{z}$, the decoder then generates an output sequence $(y_1,\ldots ,y_m)$ of symbols one element at a time.

At each step the model is auto-regressive, consuming the previously generated symbols as additional input when generating the next.

The Transformer follows this overall architecture using stacked self-attention and point-wise, fully connected layers for both the encoder and decoder, shown in the left and right halves of Figure 1, respectively.

### 3.1 Encoder and Decoder Stacks

- Encoder:

The encoder is composed of a stack of N = 6 identical layers. Each layer has two sub-layers. The first is a multi-head self-attention mechanism, and the second is a simple, position-wise fully connected feed-forward network.

We employ a residual connection around each of the two sub-layers, followed by layer normalization. That is, the output of each sub-layer is $LayerNorm(x + Sublayer(x))$, where $Sublayer(x)$ is the function implemented by the sub-layer itself.

To facilitate these residual connections, all sub-layers in the model, as well as the embedding layers, produce outputs of dimension $d_{model}=512$

- Decoder:

The decoder is also composed of a stack of N = 6 identical layers. In addition to the two sub-layers in each encoder layer, the decoder inserts a third sub-layer, which performs multi-head attention over the output of the encoder stack.

Similar to the encoder, we employ residual connections around each of the sub-layers, followed by layer normalization. We also modify the self-attention sub-layer in the decoder stack to prevent positions from attending to subsequent positions.

This masking, combined with fact that the output embeddings are offset by one position, ensures that the predictions for position i can depend only on the known outputs at positions less than i.

### 3.2 Attention

An attention function can be described as mapping a query and a set of key-value pairs to an output, where the query, keys, values, and output are all vectors. 

The output is computed as a weighted sum of the values, where the weight assigned to each value is computed by a compatibility function of the query with the corresponding key.

#### 3.2.1 Scaled Dot-Product Attention

We call our particular attention "Scaled Dot-Product Attention" (Figure 2). The input consists of queries and keys of dimension $d_k$, and values of dimension $d_v$. We compute the dot products of the query with all keys, divide each by $\sqrt{d_k}$, and apply a softmax function to obtain the weights on the values.

In practice, we compute the attention function on a set of queries simultaneously, packed together into a matrix Q. The keys and values are also packed together into matrices K and V. We compute the matrix of outputs as:

$$
\text{Attention}(Q,K,V)=\text{softmax}(\frac{QK^T}{\sqrt{d_k}})V
$$

The two most commonly used attention functions are additive attention, and dot-product (multi-plicative) attention. Dot-product attention is identical to our algorithm, except for the scaling factor of $\frac{1}{\sqrt{d}}$. Additive attention computes the compatibility function using a feed-forward network with a single hidden layer.

While the two are similar in theoretical complexity, dot-product attention is much faster and more space-efficient in practice, since it can be implemented using highly optimized matrix multiplication code.

While for small values of $d_k$ the two mechanisms perform similarly, additive attention outperforms dot product attention without scaling for larger values of $d_k$.

We suspect that for large values of $d_k$, the dot products grow large in magnitude, pushing the softmax function into regions where it has extremely small gradients. To counteract this effect, we scale the dot products by $\frac{1}{\sqrt{d}}$.

To illustrate why the dot products get large, assume that the components of q and k are independent random variables with mean 0 and variance 1. Then their dot product, $q\cdot k=\sum_{i=1}^{d_k}q_ik_i$, has mean 0 and variance $d_k$.

#### 3.2.2 Multi-Head Attention

Instead of performing a single attention function with $d_{model}$-dimensional keys, values and queries, we found it beneficial to linearly project the queries, keys and values h times with different, learned linear projections to $d_k$, $d_k$ and $d_v$ dimensions, respectively.

On each of these projected versions of queries, keys and values we then perform the attention function in parallel, yielding $d_v$-dimensional output values. These are concatenated and once again projected, resulting in the final values, as depicted in Figure 2.

Multi-head attention allows the model to jointly attend to information from different representation subspaces at different positions. With a single attention head, averaging inhibits this.

$$
\mathrm{MultiHead}(Q,K,V)=\mathrm{Concat}(\mathrm{head}_1,...,\mathrm{head}_\mathrm{h})W^O \\
\mathrm{head_i}=\mathrm{Attention}(QW_i^Q,KW_i^K,VW_i^V)
$$

Where the projections are parameter matrices $W_{i}^{Q}\in\mathbb{R}^{d_{model}\times d_{k}},W_{i}^{K}\in\mathbb{R}^{d_{model}\times d_{k}},W_{i}^{V}\in\mathbb{R}^{d_{model}\times d_{v}}$ and $W^{O}\in\mathbb{R}^{hd_v\times d_{model}}$.

In this work we employ h = 8 parallel attention layers, or heads. For each of these we use $d_k=d_v=d_{model}/h=64$. Due to the reduced dimension of each head, the total computational cost is similar to that of single-head attention with full dimensionality.

#### 3.2.3 Applications of Attention in our Model

The Transformer uses multi-head attention in three different ways:

- In "encoder-decoder attention" layers, the queries come from the previous decoder layer, and the memory keys and values come from the output of the encoder. This allows every position in the decoder to attend over all positions in the input sequence. This mimics the typical encoder-decoder attention mechanisms in sequence-to-sequence models.
- The encoder contains self-attention layers. In a self-attention layer all of the keys, values and queries come from the same place, in this case, the output of the previous layer in the encoder. Each position in the encoder can attend to all positions in the previous layer of the encoder.
- Similarly, self-attention layers in the decoder allow each position to attend to all positions in the decoder up to and including that position. We need to prevent leftward information flow in the decoder to preserve the auto-regressive property. We implement this inside of scaled dot-product attention by masking out (setting to $-\infty$) all values in the input of the softmax which correspond to illegal connections. See Figure 2.

### 3.3 Position-wise Feed-Forward Networks

In addition to attention sub-layers, each of the layers in our encoder and decoder contains a fully connected feed-forward network, which is applied to each position separately and identically. This consists of two linear transformations with a ReLU activation in between.

$$
\mathrm{FFN}(x)=\max(0,xW_1+b_1)W_2+b_2
$$

While the linear transformations are the same across different positions, they use different parameters from layer to layer. Another way of describing this is as two convolutions with kernel size 1. The dimensionality of input and output is $d_{model}=512$, and the inner-layer has dimensionality $d_{ff}=2048$.

### 3.4 Embeddings and Softmax

Similarly to other sequence transduction models, we use learned embeddings to convert the input tokens and output tokens to vectors of dimension $d_{model}$. We also use the usual learned linear transformation and softmax function to convert the decoder output to predicted next-token probabilities. In our model, we share the same weight matrix between the two embedding layers and the pre-softmax linear transformation. In the embedding layers, we multiply those weights by $d_{model}$.

### 3.5 Positional Encoding

Since our model contains no recurrence and no convolution, in order for the model to make use of the order of the sequence, we must inject some information about the relative or absolute position of the tokens in the sequence.

To this end, we add "positional encodings" to the input embeddings at the bottoms of the encoder and decoder stacks. The positional encodings have the same dimension $d_{model}$ as the embeddings, so that the two can be summed. There are many choices of positional encodings, learned and fixed.

In this work, we use sine and cosine functions of different frequencies:

$$
\begin{aligned}
PE_{(pos,2i)}&=\sin(pos/10000^{2i/d_{model}})\\
PE_{(pos,2i+1)}&=\cos(pos/10000^{2i/d_{model}})
\end{aligned}
$$

where pos is the position and i is the dimension. That is, each dimension of the positional encoding corresponds to a sinusoid. The wavelengths form a geometric progression from $2\pi$ to $10000-2\pi$.

We chose this function because we hypothesized it would allow the model to easily learn to attend by relative positions, since for any fixed offset k, $PE_{pos+k}$ can be represented as a linear function of $PE_{pos}$.

We also experimented with using learned positional embeddings instead, and found that the two versions produced nearly identical results. We chose the sinusoidal version because it may allow the model to extrapolate to sequence lengths longer than the ones encountered during training.

## 5 Training

### 5.3 Optimizer

We used the Adam optimizer with $\beta_1=0.9,\beta_2=0.98,\epsilon=10^{-9}$. We varied the learning rate over the course of training, according to the formula:

$$
lrate=d_{model}^{-0.5}\cdot\min(step\_num^{-0.5},step\_num\cdot warmup\_steps^{-1.5})
$$

This corresponds to increasing the learning rate linearly for the first *warmup_steps* training steps, and decreasing it thereafter proportionally to the inverse square root of the step number. We used $warmup\_steps=4000$.

### 5.4 Regularization

We employ three types of regularization during training:

- Residual Dropout

We apply dropout to the output of each sub-layer, before it is added to the sub-layer input and normalized. In addition, we apply dropout to the sums of the embeddings and the positional encodings in both the encoder and decoder stacks. For the base model, we use a rate of $P_{drop}=0.1$.

- Label Smoothing

During training, we employed label smoothing of value $\epsilon_{ls}=0.1$. This hurts perplexity, as the model learns to be more unsure, but improves accuracy and BLEU score.

## 7 Conclusion

https://github.com/tensorflow/tensor2tensor

#### Vacabulary

- facilitate: 促使
- be offset by one position: 偏移一位
- compatibility function: 兼容性函数
- consists of: 由......组成
- additive attention: 加法注意力
- scaling factor: 缩放因子
- space-efficient: 节省空间的
- outperform: 表现优于
- magnitude: 量级，重要性
- counteract: 抵消
- assume: 假设
- component: 分量
- linear projection: 线性投影
- concatenate: 连接
- depict: 描绘
- representation subspace: 表征子空间
- inhibit: 抑制
- mimic: 模仿
- including that position: 包括该位置在内
- prevent leftward information flow: 防止信息向左流动
- preserve: 保持
- illegal connections: 非法连接
- linear transformations: 线性变换
- sequence transduction models: 序列转换模型
- sinusoid: 正弦曲线
- wavelength: 波长
- geometric progression: 几何级数
- experiment with: 尝试
- learned positional embeddings: 学习到的位置嵌入
- extrapolate: 推断
- encountered: 遇到的
- the course of training: 训练过程
- thereafter: 随后
- proportionally: 按比例地
- inverse square root: 逆平方根
- regularization: 正则化
- label smoothing: 标签平滑
- perplexity: 困惑度
- unsure: 不确定性
