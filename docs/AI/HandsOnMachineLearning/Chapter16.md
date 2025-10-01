# Chapter 16. Natural Language Processing with RNNs and Attention

## Generating Shakespearean Text Using a Character RNN

Let’s download all of Shakespeare’s works data from Andrej Karpathy’s [char-rnn project](https://github.com/karpathy/char-rnn):

```python
import tensorflow as tf
shakespeare_url = "https://homl.info/shakespeare"
# shortcut URL
filepath = tf.keras.utils.get_file("shakespeare.txt", shakespeare_url)
with open(filepath) as f:
    shakespeare_text = f.read()

# extra code - print the first few lines as follows:
'''
First Citizen:
Before we proceed any further, hear me speak.

All:
Speak, speak.
'''
print(shakespeare_text[:80])

# extra code – shows all 39 distinct characters (after converting to lower case)
print("".join(sorted(set(shakespeare_text.lower()))))

# use TextVectorization layer to encode text. 
# set split="character" to get character-level encoding rather than the default word-level encoding.
# set standardize="lower" to convert the text to lowercase.
text_vec_layer = tf.keras.layers.TextVectorization(split="character", standardize="lower")
text_vec_layer.adapt([shakespeare_text])
encoded = text_vec_layer([shakespeare_text])[0]

# Each character is mapped to an integer, starting at 2. The TextVectorization layer reserved the value 0 for padding tokens, and it reserved 1 for unknown characters.
# We won’t need either of these tokens, so let’s subtract 2 from the character IDs.
encoded -= 2 # drop tokens 0 (pad) and 1 (unknown), which we will not use
# compute the number of distinct characters.
n_tokens = text_vec_layer.vocabulary_size() - 2 # number of distinct chars = 39
# compute the total number of characters.
dataset_size = len(encoded) # total number of chars = 1,115,394

# The targets will be similar to the inputs, but shifted by one time step into the "future".
# For example, the inputs is "to be or not to b", and the corresponding target is "o be or not to be".
# Let’s write a small utility function to convert a long sequence of character IDs into a dataset of input/target window pairs:
def to_dataset(sequence, length, shuffle=False, seed=None, batch_size=32):
    ds = tf.data.Dataset.from_tensor_slices(sequence)
    ds = ds.window(length + 1, shift=1, drop_remainder=True)
    ds = ds.flat_map(lambda window_ds: window_ds.batch(length + 1))
    if shuffle:
        ds = ds.shuffle(buffer_size=100_000, seed=seed)
    ds = ds.batch(batch_size)
    return ds.map(lambda window: (window[:, :-1], window[:, 1:])).prefetch(1)

# extra code – a simple example using to_dataset()
# There's just one sample in this dataset: the input represents "to b" and the output represents "o be"
print(list(to_dataset(text_vec_layer(["To be"])[0], length=4)))

# We set the window length to 100, but you can try tuning it. 
# The RNN will not be able to learn any pattern longer than length, so don’t make it too small.(RNN不能学习长于窗口长度的模式)
length = 100
tf.random.set_seed(42)
# We will use roughly 90% of the text for training, 5% for validation, and 5% for testing:
train_set = to_dataset(encoded[:1_000_000], length=length, shuffle=True, seed=42)
valid_set = to_dataset(encoded[1_000_000:1_060_000], length=length)
test_set = to_dataset(encoded[1_060_000:], length=length)

tf.random.set_seed(42)  # extra code – ensures reproducibility on CPU (确保可再现性)
# Let’s build and train a model with one GRU layer composed of 128 units:
# (1) Use an Embedding layer as the first layer, to encode the character IDs:
# The input dimensions is the number of distinct character IDs, and the output dimensions is a hyperparameter (we’ll set it to 16).
# The inputs of Embedding layer will be 2D tensors of shape [batch size, window length], the output will be a 3D tensor of shape [batch size, window length, embedding size].
# (2) Use a Dense layer for the output layer:
# It must have 39 units (n_tokens) because there are 39 distinct characters in the text, and we want to output a probability for each possible character (at each time step).
# The 39 output probabilities should sum up to 1, so we apply the softmax activation function to the outputs of the Dense layer.
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(input_dim=n_tokens, output_dim=16),
    tf.keras.layers.GRU(128, return_sequences=True),
    tf.keras.layers.Dense(n_tokens, activation="softmax")
])
# compile this model, using the "sparse_categorical_crossentropy" loss and a Nadam optimizer.
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam", metrics=["accuracy"])
# use a ModelCheckpoint callback to save the best model (in terms of validation accuracy) as training progresses.
model_ckpt = tf.keras.callbacks.ModelCheckpoint(
    "my_shakespeare_model", monitor="val_accuracy", save_best_only=True)
history = model.fit(train_set, validation_data=valid_set, epochs=10, callbacks=[model_ckpt])

# This model does not handle text preprocessing, so let’s wrap it in a final model containing the tf.keras.layers.TextVectorization layer as the first layer,
# plus a tf.keras.layers.Lambda layer to subtract 2 from the character IDs since we’re not using the padding and unknown tokens.
shakespeare_model = tf.keras.Sequential([
    text_vec_layer,
    tf.keras.layers.Lambda(lambda X: X - 2), # no <PAD> or <UNK> tokens
    model
])

# Let’s use it to predict the next character in a sentence
y_proba = shakespeare_model.predict(["To be or not to b"])[0, -1]
y_pred = tf.argmax(y_proba) # choose the most probable character ID
print(text_vec_layer.get_vocabulary()[y_pred + 2])  # print 'e'

# extra code – use tf.random.categorical() function samples the next character randomly, with a probability equal to the estimated probability
log_probas = tf.math.log([[0.5, 0.4, 0.1]]) # probas = 50%, 40%, and 10%
tf.random.set_seed(42)
print(tf.random.categorical(log_probas, num_samples=8)) # draw 8 samples
# <tf.Tensor: shape=(1, 8), dtype=int64, numpy=array([[0, 1, 0, 2, 1, 0, 0, 1]])>

# Use the next_char() function to pick the next character to add to the input text
def next_char(text, temperature=1):
    y_proba = shakespeare_model.predict([text])[0, -1:]
    # To have more control over the diversity of the generated text, we can divide the logits by a number called the temperature. (控制生成文本的多样性)
    # A temperature close to zero favors high-probability characters, while a high temperature gives all characters an equal probability.
    # Lower temperatures are typically preferred when generating fairly rigid and precise text, such as mathematical equations, while higher temperatures are preferred when generating more diverse and creative text.(低temperature有利于生成死板而精确的文本，高temperature有利于生成多样化而有创造性的文本)
    rescaled_logits = tf.math.log(y_proba) / temperature
    char_id = tf.random.categorical(rescaled_logits, num_samples=1)[0, 0]
    return text_vec_layer.get_vocabulary()[char_id + 2]

# repeatedly call next_char() to get the next character and append it to the given text.
def extend_text(text, n_chars=50, temperature=1):
    for _ in range(n_chars):
        text += next_char(text, temperature)
    return text

# Let’s try with different temperature values:
tf.random.set_seed(42)
print(extend_text("To be or not to be", temperature=0.01))
'''
To be or not to be the duke
as it is a proper strange death,
and the
'''
print(extend_text("To be or not to be", temperature=1))
'''
To be or not to behold?
second push:
gremio, lord all, a sistermen,
'''
print(extend_text("To be or not to be", temperature=100))
'''
To be or not to bef ,mt'&o3fpadm!$
wh!nse?bws3est--vgerdjw?c-y-ewznq
'''
```

### Generating Fake Shakespearean Text

To generate new text using the char-RNN model, we could feed it some text, make the model predict the most likely next letter, add it to the end of the text, then give the extended text to the model to guess the next letter, and so on. This is called **greedy decoding**.(要使用char-RNN模型生成新文本，我们可以输入一些文本，让模型预测最有可能的下一个字母，并将其添加到文本末尾，然后将扩展文本交给模型，让其猜测下一个字母，以此类推。这就是所谓的贪婪解码。)

To generate more convincing text, a common technique is to sample only from the top k characters, or only from the smallest set of top characters whose total probability exceeds some threshold (this is called **nucleus sampling**). (为了生成更有说服力的文本，一种常用的技术是只对前k个字符进行采样，或者只对总概率超过某个阈值的前几个字符的最小集合进行采样，这称为核采样。)

## Stateful RNN

- **Stateless RNNs**: at each training iteration the model starts with a hidden state full of zeros, then it updates this state at each time step, and after the last time step, it throws it away as it is not needed anymore.（无状态RNN：在每次训练迭代中，模型从一个全是零的隐藏状态开始，然后在每个时间步长更新该状态，在最后一个时间步长之后，由于不再需要该状态，就将其丢弃。）
- **Stateful RNN**: the RNN preserves this final state after processing a training batch and use it as the initial state for the next training batch. This way the model could learn long-term patterns despite only backpropagating through short sequences.（有状态RNN：RNN在处理完一个训练批次后保留这一最终状态，并将其作为下一个训练批次的初始状态。这样，尽管模型仅通过短序列进行反向传播，但能学习长期模式。）

```python
# Stateful RNN only makes sense if each input sequence in a batch starts exactly where the corresponding sequence in the previous batch left off.(每批次输入序列的起始位置要与上一批次序列的结束位置完全一致)
# So we need to build a stateful RNN is to use sequential and nonoverlapping input sequences, rather than the shuffled and overlapping sequences we used to train stateless RNNs.(有状态RNN使用连续且不重叠的输入序列，无状态RNN使用随机排列且重叠序列)
# When creating the tf.data.Dataset, we must use shift=length (instead of shift=1) when calling the window() method. Moreover, we must not call the shuffle() method.
# If we were to call batch(32), then 32 consecutive windows would be put in the same batch, and the following batch would not continue each of these windows where it left off.(调用batch(32)，那么32个连续的窗口将被放入同一个批次中，而下一个批次将不会继续这些窗口)
# The first batch would contain windows 1 to 32 and the second batch would contain windows 33 to 64, so if you consider the first window of each batch (i.e., windows 1 and 33), you can see that they are not consecutive.(第一批次包含第1到32窗口，第二批次包含第33到64窗口，如果考虑每批次第一个窗口（如第1和33窗口），就会发现它们并不是连续的)
# The simplest solution to this problem is to just use a batch size of 1. The following to_dataset_for_stateful_rnn() custom utility function uses this strategy to prepare a dataset for a stateful RNN:
def to_dataset_for_stateful_rnn(sequence, length):
    ds = tf.data.Dataset.from_tensor_slices(sequence)
    ds = ds.window(length + 1, shift=length, drop_remainder=True)
    ds = ds.flat_map(lambda window: window.batch(length + 1)).batch(1)
    return ds.map(lambda window: (window[:, :-1], window[:, 1:])).prefetch(1)

stateful_train_set = to_dataset_for_stateful_rnn(encoded[:1_000_000], length)
stateful_valid_set = to_dataset_for_stateful_rnn(encoded[1_000_000:1_060_000], length)
stateful_test_set = to_dataset_for_stateful_rnn(encoded[1_060_000:], length)

# extra code – simple example using to_dataset_for_stateful_rnn()
print(list(to_dataset_for_stateful_rnn(tf.range(10), 3)))

# extra code – shows one way to prepare a batched dataset for a stateful RNN

import numpy as np

def to_non_overlapping_windows(sequence, length):
    ds = tf.data.Dataset.from_tensor_slices(sequence)
    ds = ds.window(length + 1, shift=length, drop_remainder=True)
    return ds.flat_map(lambda window: window.batch(length + 1))

# We could chop Shakespeare’s text into 32 texts of equal length, create one dataset of consecutive input sequences for each of them, (将莎士比亚的文本切分成32个长度相等的文本，为每个文本创建一个连续输入序列的数据集)
# and finally use tf.data.Dataset.zip(datasets).map(lambda *windows: tf.stack(windows)) to create proper consecutive batches, where the n_th input sequence in a batch starts off exactly where the n_th input sequence ended in the previous batch. (一个批次中的第n个输入序列的开始正好是上一个批次中第n个输入序列的结束)
def to_batched_dataset_for_stateful_rnn(sequence, length, batch_size=32):
    parts = np.array_split(sequence, batch_size)
    datasets = tuple(to_non_overlapping_windows(part, length) for part in parts)
    ds = tf.data.Dataset.zip(datasets).map(lambda *windows: tf.stack(windows))
    return ds.map(lambda window: (window[:, :-1], window[:, 1:])).prefetch(1)

print(list(to_batched_dataset_for_stateful_rnn(tf.range(20), length=3, batch_size=2)))

# We need to set the stateful argument to True when creating each recurrent layer.
# Because the stateful RNN needs to know the batch size (since it will preserve a state for each input sequence in the batch). Therefore we must set the batch_input_shape argument in the first layer. (因为有状态RNN需要知道批次大小，所以在第一层中设置batch_input_shape)
# Note that we can leave the second dimension unspecified, since the input sequences could have any length. (batch_input_shape可以不指定第二个维度，因为输入序列可以是任何长度)
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(input_dim=n_tokens, output_dim=16,batch_input_shape=[1, None]),
    tf.keras.layers.GRU(128, return_sequences=True, stateful=True),
    tf.keras.layers.Dense(n_tokens, activation="softmax")
])

# At the end of each epoch, we need to reset the states before we go back to the beginning of the text. For this, we can use a small custom Keras callback: (在每个epoch结束时，我们需要再回到文本开头之前的状态。)
class ResetStatesCallback(tf.keras.callbacks.Callback):
    def on_epoch_begin(self, epoch, logs):
        self.model.reset_states()

# extra code – use a different directory to save the checkpoints
model_ckpt = tf.keras.callbacks.ModelCheckpoint(
    "my_stateful_shakespeare_model",
    monitor="val_accuracy",
    save_best_only=True)

# Now we can compile the model and train it using our callback:
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam",
        metrics=["accuracy"])
history = model.fit(stateful_train_set, validation_data=stateful_valid_set,
        epochs=10, callbacks=[ResetStatesCallback(), model_ckpt])

# After this model is trained, it will only be possible to use it to make predictions for batches of the same size as were used during training. (该模型只能对与训练时相同大小的批次进行预测)
# To avoid this restriction, create an identical stateless model, and copy the stateful model’s weights to this model.
stateless_model = tf.keras.Sequential([
    tf.keras.layers.Embedding(input_dim=n_tokens, output_dim=16),
    tf.keras.layers.GRU(128, return_sequences=True),
    tf.keras.layers.Dense(n_tokens, activation="softmax")
])

stateless_model.build(tf.TensorShape([None, None]))
stateless_model.set_weights(model.get_weights())

shakespeare_model = tf.keras.Sequential([
    text_vec_layer,
    tf.keras.layers.Lambda(lambda X: X - 2),  # no <PAD> or <UNK> tokens
    stateless_model
])

tf.random.set_seed(42)
print(extend_text("to be or not to be", temperature=0.01))
'''
to be or not to be so in the world and the strangeness
to see the wo
'''
```

## Sentiment Analysis

The IMDb dataset consists of 50,000 movie reviews in English (25,000 for training, 25,000 for testing) extracted from the famous Internet Movie Database, along with a simple binary target for each review indicating whether it is negative (0) or positive (1).

```python
import tensorflow_datasets as tfds

# Let’s load the IMDb dataset using the TensorFlow Datasets library. We’ll use the first 90% of the training set for training, and the remaining 10% for validation:
raw_train_set, raw_valid_set, raw_test_set = tfds.load(
    name="imdb_reviews",
    split=["train[:90%]", "train[90%:]", "test"],
    as_supervised=True
)
tf.random.set_seed(42)
train_set = raw_train_set.shuffle(5000, seed=42).batch(32).prefetch(1)
valid_set = raw_valid_set.batch(32).prefetch(1)
test_set = raw_test_set.batch(32).prefetch(1)

# Let’s inspect a few reviews:
for review, label in raw_train_set.take(4):
    print(review.numpy().decode("utf-8"))
    print("Label:", label.numpy())

# We will limit the vocabulary to 1,000 tokens, including the most frequent 998 words plus a padding token and a token for unknown words, since it’s unlikely that very rare words will be important for this task, and limiting the vocabulary size will reduce the number of parameters the model needs to learn:（我们把词汇量限制在1000个，包括最常见的998个单词加上一个填充标记和一个未知单词标记，因为非常罕见的单词不太可能对这项任务很重要，而且限制词汇量可以减少模型需要学习的参数数量）
vocab_size = 1000
# This time we will chop it into words instead of characters. For this, we can use the tf.keras.layers.TextVectorization layer again.
text_vec_layer = tf.keras.layers.TextVectorization(max_tokens=vocab_size)
text_vec_layer.adapt(train_set.map(lambda reviews, labels: reviews))

# Finally, we can create the model and train it:
embed_size = 128
tf.random.set_seed(42)
# The embedding matrix needs to have one row per token in the vocabulary (vocab_size) and one column per embedding dimension (this example uses 128 dimensions, but this is a hyperparameter you could tune). (embedding矩阵为词汇表中的每个token设置一行，为每个embedding维度设置一列。)
# We use a Dense layer with a single neuron and the sigmoid activation function, since this is a binary classification task: the model’s output will be the estimated probability that the review expresses a positive sentiment regarding the movie.
model = tf.keras.Sequential([
    text_vec_layer,
    tf.keras.layers.Embedding(vocab_size, embed_size),
    tf.keras.layers.GRU(128),
    tf.keras.layers.Dense(1, activation="sigmoid")
])
model.compile(loss="binary_crossentropy", optimizer="nadam", metrics=["accuracy"])
history = model.fit(train_set, validation_data=valid_set, epochs=2)
# Sadly, if you run this code, you will generally find that the model fails to learn anything at all: the accuracy remains close to 50%.
```

BPE(byte pair encoding) works by splitting the whole training set into individual characters (including spaces), then repeatedly merging the most frequent adjacent pairs until the vocabulary reaches the desired size.(字节对编码的工作原理是将整个训练集分割成单个字符，然后重复合并最频繁的相邻字符对，直到词汇量达到所需的大小。)

The paper proposed a novel regularization technique called *subword regularization*, which improves accuracy and robustness by introducing some randomness in tokenization during training: for example, "New England" may be tokenized as "New" + "England", or "New" + "Eng" + "land", or simply "New England".(该论文提出了一种新颖的叫做子词正则化的技术，通过训练时在分词中引入一些随机性来提高准确性和鲁棒性。)

The TensorFlow Text library also implements various tokenization strategies, including WordPiece(a variant of BPE).(Text 库实现了多种分词策略，包括WordPiece，它是BPE的一种变体。)

The reviews have different lengths, so when the TextVectorization layer converts them to sequences of token IDs, it pads the shorter sequences using the padding token (with ID 0) to make them as long as the longest sequence in the batch.(评论数据具有不同的长度，当TextVectorization将其转换为token ID序列时，会使用0填充较短的序列，使其与最长的序列一样长。)

Even though we're using a GRU layer, which is much better than a SimpleRNN layer, its short-term memory is still not great, so when it goes through many padding tokens, it ends up forgetting what the review was about!(GRU层经历了许多填充标记(也就是0)后，最终会忘记评论的内容！)

One solution is to feed the model with batches of equal-length sentences. Another solution is to make the RNN ignore the padding tokens. This can be done using masking.(一种解决方案是向模型输入成批的等长句子。另一种解决方案是让RNN忽略填充标记，这可以通过masking来实现。)

### Masking

```python
embed_size = 128
tf.random.set_seed(42)
# Simply add mask_zero=True when creating the Embedding layer. This means that padding tokens (whose ID is 0) will be ignored by all downstream layers. 
model = tf.keras.Sequential([
    text_vec_layer,
    tf.keras.layers.Embedding(vocab_size, embed_size, mask_zero=True),
    tf.keras.layers.GRU(128),
    tf.keras.layers.Dense(1, activation="sigmoid")
])
model.compile(loss="binary_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
history = model.fit(train_set, validation_data=valid_set, epochs=5)
```

The way this works is that the Embedding layer creates a **mask tensor** equal to tf.math.not_equal(inputs, 0): it is a Boolean tensor with the same shape as the inputs, and it is equal to False anywhere the token IDs are 0, or True otherwise.(掩码张量是一个布尔张量，形状与输入相同，在token ID为0的位置等于False，其他位置等于True。)

This mask tensor is then automatically propagated by the model to the next layer. If that layer’s call() method has a mask argument, then it automatically receives the mask. This allows the layer to ignore the appropriate time steps. (掩码张量将由模型自动传播到下一层。如果该层的call()方法有mask参数，就自动接收掩码。这样该层就可以忽略相应的时间步长。)

If the layer’s supports_masking attribute is True, then the mask is automatically propagated to the next layer.(如果某层的supports_masking的属性为True，则掩码会自动传播到下一层。如果supports_masking的属性为False掩码就不再进一步传播)

Similarly, if you set mask_zero=True when creating the Embedding layer in the sentiment analysis model we just built, then the GRU layer will receive and use the mask automatically, but it will not propagate it any further, since return_sequences is not set to True.(如果情感分析模型中创建嵌入层时设置mask_zero=True，那么GRU层将自动接收并使用掩码，但return_sequences没有设置为True，所以掩码不会进一步传播。)

**TIP**: Some layers need to update the mask before propagating it to the next layer: they do so by implementing the compute_mask() method, which takes two arguments: the inputs and the previous mask. (有些层需要在掩码传播到下一层之前更新掩码：它们通过实现compute_mask()方法来更新掩码，该方法需要两个参数：输入和上一层的掩码。)

If the mask propagates all the way to the output, then it gets applied to the losses as well, so the masked time steps will not contribute to the loss (their loss will be 0).(如果掩码一直传播到输出，那么它也会应用于损失，因此被屏蔽的时间步长不会对损失产生影响)

If you want to implement your own custom layer with masking support, you should add a mask argument to the call() method.

Additionally, if the mask must be propagated to the next layers, then you should set self.supports_masking=True in the constructor.

If the mask must be updated before it is propagated, then you must implement the compute_mask() method.

`tf.keras.layers.Masking layer` sets the mask to `tf.math.reduce_any(tf.math.not_equal(X,0), axis=-1)`, meaning that time steps where the last dimension is full of zeros will be masked out in subsequent layers.(`tf.keras.layer.Masking`层的后续层中，最后一个维度全为零的时间步长将被屏蔽掉。)

Using masking layers and automatic mask propagation works best for simple models.It will not always work for more complex models, such as when you need to mix Conv1D layers with recurrent layers.

```python
# The following model is built using the functional API and handles masking manually. 
# It also adds a bit of dropout since the previous model was overfitting slightly.
inputs = tf.keras.layers.Input(shape=[], dtype=tf.string)
token_ids = text_vec_layer(inputs)
mask = tf.math.not_equal(token_ids, 0)
Z = tf.keras.layers.Embedding(vocab_size, embed_size)(token_ids)
Z = tf.keras.layers.GRU(128, dropout=0.2)(Z, mask=mask)
outputs = tf.keras.layers.Dense(1, activation="sigmoid")(Z)
model = tf.keras.Model(inputs=[inputs], outputs=[outputs])

# extra code – compiles and trains the model, as usual
model.compile(loss="binary_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
history = model.fit(train_set, validation_data=valid_set, epochs=5)
```

One last approach to masking is to feed the model with ragged tensors.

```python
# Set ragged=True when creating the TextVectorization layer, so that the input sequences are represented as ragged tensors.
text_vec_layer_ragged = tf.keras.layers.TextVectorization(
    max_tokens=vocab_size, ragged=True)
text_vec_layer_ragged.adapt(train_set.map(lambda reviews, labels: reviews))

# Compare this ragged tensor representation with the regular tensor representation, which uses padding tokens:
print(text_vec_layer_ragged(["Great movie!", "This is DiCaprio's best role."]))
# <tf.RaggedTensor [[86, 18], [11, 7, 1, 116, 217]]>

print(text_vec_layer(["Great movie!", "This is DiCaprio's best role."]))
'''
<tf.Tensor: shape=(2, 5), dtype=int64, numpy=
array([[ 86,  18,   0,   0,   0],
       [ 11,   7,   1, 116, 217]])>
'''

embed_size = 128
tf.random.set_seed(42)
model = tf.keras.Sequential([
    text_vec_layer_ragged,
    tf.keras.layers.Embedding(vocab_size, embed_size),
    tf.keras.layers.GRU(128),
    tf.keras.layers.Dense(1, activation="sigmoid")
])
model.compile(loss="binary_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
history = model.fit(train_set, validation_data=valid_set, epochs=5)
```

However, as of early 2022,the support for ragged tensors in Keras is still fairly recent, so there are a few rough edges. For example, it is currently not possible to use ragged tensors as targets when running on the GPU. (截至2022年初，ragged tensors不能在GPU上使用)

If you use the `tf.keras.callbacks.TensorBoard()` callback, you can visualize the embeddings in TensorBoard as they are being learned: it is fascinating to see words like "awesome" and "amazing" gradually cluster on one side of the embedding space, while words like "awful" and "terrible" cluster on the other side.(可以在TensorBoard中可视化embedding：看到awesome和amazing这样的词逐渐聚集在嵌入空间的一侧，而awful和terrible这样的词聚集在另一侧。)

Some words are not as positive as you might expect, such as the word "good", presumably because many negative reviews contain the phrase "not good".

## Reusing Pretrained Embeddings and Language Models

```python
import os
import tensorflow_hub as hub

# You must set the TFHUB_CACHE_DIR environment variable to a directory of your choice: the modules will then be saved there, and only downloaded once.
os.environ["TFHUB_CACHE_DIR"] = "my_tfhub_cache"
# Let’s build a classifier based on the Universal Sentence Encoder. Conveniently, the model is available on TensorFlow Hub.
# The last part of the TensorFlow Hub module URL specifies that we want version 4 of the model. This versioning ensures that if a new module version is released on TF Hub, it will not break our model.
# We set trainable=True when creating the hub.KerasLayer. This way, the pretrained Universal Sentence Encoder is fine-tuned during training: some of its weights are tweaked via backprop.(设置trainable=True，这样预训练模型就可以在训练过程中进行微调)
model = tf.keras.Sequential([
    hub.KerasLayer("https://tfhub.dev/google/universal-sentence-encoder/4",
                   trainable=True, dtype=tf.string, input_shape=[]),
    tf.keras.layers.Dense(64, activation="relu"),
    tf.keras.layers.Dense(1, activation="sigmoid")
])
model.compile(loss="binary_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
model.fit(train_set, validation_data=valid_set, epochs=10)
```

## An Encoder–Decoder Network for Neural Machine Translation

The architecture of [NMT model](https://homl.info/103) is as follows: English sentences are fed as inputs to the encoder, and the decoder outputs the Spanish translations. Note that the Spanish translations are also used as inputs to the decoder during training, but shifted back by one step. In other words, during training the decoder is given as input the word that it should have output at the previous step, regardless of what it actually output. This is called **teacher forcing**. (NMT模型的结构如下：英语句子作为编码器的输入，解码器输出西班牙语译文。请注意，在训练过程中，西班牙语译文也被用作解码器的输入，但是后移一个步长。换句话说，在训练过程中，解码器的输入是它在上一步应该输出的目标词汇，而不管它实际输出了什么，这被称为teacher forcing)

```python
# Download a dataset of English/Spanish sentence pairs:
url = "https://storage.googleapis.com/download.tensorflow.org/data/spa-eng.zip"
path = tf.keras.utils.get_file("spa-eng.zip", origin=url, cache_dir="datasets", extract=True)
text = (Path(path).with_name("spa-eng") / "spa.txt").read_text()

import numpy as np

# Each line contains an English sentence and the corresponding Spanish translation, separated by a tab.
# Remove the Spanish characters “¡” and “¿”, which the TextVectorization layer doesn’t handle.
text = text.replace("¡", "").replace("¿", "")
# Split them into two separate lists, one per language.
pairs = [line.split("\t") for line in text.splitlines()]
np.random.shuffle(pairs)
sentences_en, sentences_es = zip(*pairs)  # separates the pairs into 2 lists

# Let’s take a look at the first three sentence pairs:
for i in range(3):
    print(sentences_en[i], "=>", sentences_es[i])
'''
How boring! => Qué aburrimiento!
I love sports. => Adoro el deporte.
Would you like to swap jobs? => Te gustaría que intercambiemos los trabajos?
'''

# Next, let’s create two TextVectorization layers — one per language — and adapt them to the text.
# We limit the vocabulary size to 1,000. That’s because the training set is not very large, and because using a small value will speed up training.
vocab_size = 1000
# Since all sentences in the dataset have a maximum of 50 words, we set output_sequence_length to 50: 
# this way the input sequences will automatically be padded with zeros until they are all 50 tokens long. 
# If there was any sentence longer than 50 tokens in the training set, it would be cropped to 50 tokens. (长于50个token的句子会被裁剪为50个token)
max_length = 50
text_vec_layer_en = tf.keras.layers.TextVectorization(
    vocab_size, output_sequence_length=max_length)
text_vec_layer_es = tf.keras.layers.TextVectorization(
    vocab_size, output_sequence_length=max_length)
text_vec_layer_en.adapt(sentences_en)
# For the very first word, the decoder is given the start-of-sequence (SOS) token, and the decoder is expected to end the sentence with an end-of-sequence (EOS) token.
# For the Spanish text, we add “startofseq” and “endofseq” to each sentence when adapting the TextVectorization layer: we will use these words as SOS and EOS tokens.
text_vec_layer_es.adapt([f"startofseq {s} endofseq" for s in sentences_es])

# Let’s inspect the first 10 tokens in both vocabularies. 
# They start with the padding token, the unknown token, the SOS and EOS tokens (only in the Spanish vocabulary), 
# then the actual words, sorted by decreasing frequency. (实际的单词按频率递减排序)
print(text_vec_layer_en.get_vocabulary()[:10])
['', '[UNK]', 'the', 'i', 'to', 'you', 'tom', 'a', 'is', 'he']
print(text_vec_layer_es.get_vocabulary()[:10])
['', '[UNK]', 'startofseq', 'endofseq', 'de', 'que', 'a', 'no', 'tom', 'la']

# We will use the first 100,000 sentence pairs for training, and the rest for validation.
X_train = tf.constant(sentences_en[:100_000])
X_valid = tf.constant(sentences_en[100_000:])
# The decoder’s inputs are the Spanish sentences plus an SOS token prefix.
X_train_dec = tf.constant([f"startofseq {s}" for s in sentences_es[:100_000]])
X_valid_dec = tf.constant([f"startofseq {s}" for s in sentences_es[100_000:]])
# The targets are the Spanish sentences plus an EOS suffix.
Y_train = text_vec_layer_es([f"{s} endofseq" for s in sentences_es[:100_000]])
Y_valid = text_vec_layer_es([f"{s} endofseq" for s in sentences_es[100_000:]])

# Translation model requires two text inputs, one for the encoder and one for the decoder.
encoder_inputs = tf.keras.layers.Input(shape=[], dtype=tf.string)
decoder_inputs = tf.keras.layers.Input(shape=[], dtype=tf.string)

# The embedding size is a hyperparameter you can tune
embed_size = 128
# encode these sentences using the TextVectorization layers, followed by an Embedding layer for each language, with mask_zero=True to ensure masking is handled automatically.
encoder_input_ids = text_vec_layer_en(encoder_inputs)
decoder_input_ids = text_vec_layer_es(decoder_inputs)
# Each word is initially represented by its ID (e.g., 854 for the word "soccer"). Next, an Embedding layer returns the word embedding.
encoder_embedding_layer = tf.keras.layers.Embedding(vocab_size, embed_size,
                                                    mask_zero=True)
decoder_embedding_layer = tf.keras.layers.Embedding(vocab_size, embed_size,
                                                    mask_zero=True)
encoder_embeddings = encoder_embedding_layer(encoder_input_ids)
decoder_embeddings = decoder_embedding_layer(decoder_input_ids)

# Let’s create the encoder and pass it the embedded inputs.
# To keep things simple, we just used a single LSTM layer, but you could stack several of them.
# Set return_state=True to get a reference to the layer’s final state. (设置return_state=True以获得该层最终状态的引用)
encoder = tf.keras.layers.LSTM(512, return_state=True)
# Since we’re using an LSTM layer, there are actually two states: the short-term state and the long-term state.(LSTM层有两种状态：短期状态和长期状态)
# The layer returns these states separately, which is why we had to write *encoder_state to group both states in a list.⁠ (该层分别返回这两种状态，所以我们必须写*encoder_state来将这两种状态组合在一个列表中。)
encoder_outputs, *encoder_state = encoder(encoder_embeddings)

# Use this (double) state as the initial state of the decoder.
decoder = tf.keras.layers.LSTM(512, return_sequences=True)
decoder_outputs = decoder(decoder_embeddings, initial_state=encoder_state)

# Next, we can pass the decoder’s outputs through a Dense layer with the softmax activation function to get the word probabilities for each step:
output_layer = tf.keras.layers.Dense(vocab_size, activation="softmax")
Y_proba = output_layer(decoder_outputs)

model = tf.keras.Model(inputs=[encoder_inputs, decoder_inputs],
                       outputs=[Y_proba])
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
model.fit((X_train, X_train_dec), Y_train, epochs=10,
          validation_data=((X_valid, X_valid_dec), Y_valid))

# To translate new English sentences to Spanish, We can just call the model multiple times, predicting one extra word at each round.
# The function simply keeps predicting one word at a time, gradually completing the translation, and it stops once it reaches the EOS token.
def translate(sentence_en):
    translation = ""
    for word_idx in range(max_length):
        X = np.array([sentence_en])  # encoder input
        X_dec = np.array(["startofseq " + translation])  # decoder input
        y_proba = model.predict((X, X_dec))[0, word_idx]  # last token's probas
        predicted_word_id = np.argmax(y_proba)
        predicted_word = text_vec_layer_es.get_vocabulary()[predicted_word_id]
        if predicted_word == "endofseq":
            break
        translation += " " + predicted_word
    return translation.strip()

print(translate("I like soccer"))
# 'me gusta el fútbol'

# If you try playing with this model for a while, you will find that it’s not bilingual yet, and in particular it really struggles with longer sentences.
print(translate("I like soccer and also going to the beach"))
# 'me gusta el fútbol y a veces mismo al bus'
```

**OPTIMIZING THE OUTPUT LAYER**

When the output vocabulary is large, outputting a probability for each and every possible word can be quite slow.

To avoid this, one solution is to look only at the logits output by the model for the correct word and for a random sample of incorrect words, then compute an approximation of the loss based only on these logits. This **sampled softmax** technique was introduced in 2015 by Sébastien Jean et al.⁠ In TensorFlow you can use the tf.nn.sampled_softmax_loss() function for this during training and use the normal softmax function at inference time (sampled softmax cannot be used at inference time because it requires knowing the target). (一种解决方案是sampled softmax：只查看模型输出的正确单词和错误单词随机样本的对数，然后只根据这些对数计算损失的近似值。)

Another thing you can do to speed up training — which is compatible with sampled softmax — is to tie the weights of the output layer to the transpose of the decoder’s embedding matrix. (另一个加快训练速度的方法是将输出层的权重与解码器嵌入矩阵的转置联系起来，这与sampled softmax兼容。)

### Bidirectional RNNs

One solution is to run two recurrent layers on the same inputs, one reading the words from left to right and the other reading them from right to left, then combine their outputs at each time step, typically by concatenating them. This is what a **bidirectional recurrent layer** does.(双向循环层是在相同的输入上运行两个循环层，一个从左到右读取词汇，另一个从右到左读取词汇，然后在每个时间步长上合并输出，通常是将它们连接起来。)

```python
# To implement a bidirectional recurrent layer in Keras, just wrap a recurrent layer in a tf.keras.layers.Bidirectional layer.
encoder = tf.keras.layers.Bidirectional(
    tf.keras.layers.LSTM(256, return_state=True))

# This layer will now return four states instead of two: the final short-term and long-term states of the forward LSTM layer, and the final short-term and long-term states of the backward LSTM layer.
encoder_outputs, *encoder_state = encoder(encoder_embeddings)
# We cannot use this quadruple state directly as the initial state of the decoder’s LSTM layer, since it expects just two states (short-term and long-term).
# Instead, we can concatenate the two short-term states, and also concatenate the two long-term states:
encoder_state = [tf.concat(encoder_state[::2], axis=-1),  # short-term (0 & 2)
                 tf.concat(encoder_state[1::2], axis=-1)]  # long-term (1 & 3)

# extra code — completes the model and trains it
decoder = tf.keras.layers.LSTM(512, return_sequences=True)
decoder_outputs = decoder(decoder_embeddings, initial_state=encoder_state)
output_layer = tf.keras.layers.Dense(vocab_size, activation="softmax")
Y_proba = output_layer(decoder_outputs)
model = tf.keras.Model(inputs=[encoder_inputs, decoder_inputs],
                       outputs=[Y_proba])
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
model.fit((X_train, X_train_dec), Y_train, epochs=10,
          validation_data=((X_valid, X_valid_dec), Y_valid))

print(translate("I like soccer"))
# 'me gusta el fútbol'
```

### Beam Search

How can we give the model a chance to go back and fix mistakes it made earlier? One of the most common solutions is **beam search**: it keeps track of a short list of the k most promising sentences (say, the top three), and at each decoder step it tries to extend them by one word, keeping only the k most likely sentences. The parameter k is called the **beam width**.(集束搜索会记录一个由k个最有希望的句子（比如前三名）组成的简短列表，在解码器的每一步都会尝试将其扩展一个词，只保留k个最有可能的句子。参数k称为集束宽度。)

## Attention Mechanisms

This was the core idea in a landmark [2014 paper](https://arxiv.org/abs/1409.0473)⁠ by Dzmitry Bahdanau et al., where the authors introduced a technique that allowed the decoder to focus on the appropriate words (as encoded by the encoder) at each time step.

**NOTE**: The most common metric used in NMT is the bilingual evaluation understudy (BLEU) score, which compares each translation produced by the model with several good translations produced by humans: it counts the number of n-grams (sequences of n words) that appear in any of the target translations and adjusts the score to take into account the frequency of the produced n-grams in the target translations.(在NMT中最常用的指标是双语评估（BLEU）得分，它将模型生成的译文与人类翻译的优秀译文进行比较：计算目标译文中n-grams（由n个单词组成的序列）的数量，并根据n-grams在目标译文中出现的频率调整得分。)

The equations for these three attention mechanisms are summarized in Equation 16-1.

$$
\begin{aligned}
& \mathbf{\tilde h}_{(t)}=\sum_i\alpha_{(t,i)}\mathbf{y}_{(i)} \\
& \mathbf{with}\quad\alpha_{(t,i)}=\frac{\exp(e_{(t,i)})}{\sum_{i^\prime}\exp(e_{(t,i^\prime)})} \\
& \mathbf{and}\quad e_{(t,i)}=\begin{cases}
& \mathbf{h}_{(t)}^T\mathbf{y}_{(i)} & \mathnormal{dot} \\
& \mathbf{h}_{(t)}^T\mathbf{W}\mathbf{y}_{(i)} & \mathnormal{general} \\
& \mathbf{v}^T\tanh(\mathbf{W}[\mathbf{h}_{(t)};\mathbf{y}_{(i)}]) & \mathnormal{concat}
\end{cases}
\end{aligned}
$$

The weight $\alpha(t,i)$ is the weight of the $i^{th}$ encoder output at the $t^{th}$ decoder time step. For example, if the weight $\alpha(3,2)$ is much larger than the weights $\alpha(3,0)$ and $\alpha(3,1)$, then the decoder will pay much more attention to the encoder’s output for word #2 ("soccer") than to the other two outputs.(权重$\alpha(t,i)$是对应t个解码器下第i个编码器输出的权重。)

These $\alpha(t,i)$ weights are generated by a small neural network called an **alignment model** (or an **attention layer**), which is trained jointly with the rest of the encoder–decoder model.

It starts with a Dense layer composed of a single neuron that processes each of the encoder’s outputs, along with the decoder's previous hidden state. This layer outputs a score (or energy) for each encoder output: this score measures how well each output is aligned with the decoder’s previous hidden state.(alignment model由一个神经元组成的密集层开始，该神经元处理编码器的输出以及解码器之前的隐藏状态。该层为每个编码器输出输出一个分数：该分数衡量每个输出与解码器之前隐藏状态的匹配程度。)

This particular attention mechanism is called **Bahdanau attention** (named after the 2014 paper's first author). Since it concatenates the encoder output with the decoder's previous hidden state, it is sometimes called concatenative attention (or additive attention).(由于Bahdanau attention将编码器输出与解码器之前的隐藏状态连接起来，因此也被称为concatenative attention)

Another common attention mechanism, known as **Luong attention** or multiplicative attention, was proposed shortly after, in [2015](https://arxiv.org/abs/1508.04025),⁠ by Minh-Thang Luong et al.

Because the goal of the alignment model is to measure the similarity between one of the encoder’s outputs and the decoder’s previous hidden state, the authors proposed to simply compute the dot product of these two vectors, as this is often a fairly good similarity measure.

For this to be possible, both vectors must have the same dimensionality. The dot product gives a score, and all the scores (at a given decoder time step) go through a softmax layer to give the final weights, just like in Bahdanau attention.(编码器输出向量与解码器之前的隐藏状态向量必须具有相同的维度。点积给出一个分数，所有分数都要经过一个softmax层，以给出最终权重)

Another simplification Luong et al. proposed was to use the decoder's hidden state at the current time step rather than at the previous time step (i.e., $h_{(t)}$ rather than $h_{(t–1)}$), then to use the output of the attention mechanism (noted $\tilde h_{(t)}$) directly to compute the decoder’s predictions, rather than using it to compute the decoder's current hidden state.(Luong等人提出的另一个简化方法是使用解码器在当前时间步的隐藏状态，而不是上一个时间步的隐藏状态，然后直接使用注意力机制的输出来计算解码器的预测，而不是计算解码器当前的隐藏状态。)

The researchers also proposed a variant of the dot product mechanism where the encoder outputs first go through a fully connected layer (without a bias term) before the dot products are computed. This is called the "general" dot product approach.(研究人员还提出了点积机制的一种变体，即在计算点积之前，编码器输出首先经过一个全连接层（不含偏置项）。)

```python
# Since we will need to pass all the encoder's outputs to the Attention layer, we first need to set return_sequences=True when creating the encoder.
encoder = tf.keras.layers.Bidirectional(
    tf.keras.layers.LSTM(256, return_sequences=True, return_state=True))

# extra code – this part of the model is exactly the same as earlier
encoder_outputs, *encoder_state = encoder(encoder_embeddings)
encoder_state = [tf.concat(encoder_state[::2], axis=-1),  # short-term (0 & 2)
                 tf.concat(encoder_state[1::2], axis=-1)]  # long-term (1 & 3)
decoder = tf.keras.layers.LSTM(512, return_sequences=True)
decoder_outputs = decoder(decoder_embeddings, initial_state=encoder_state)

# Keras provides a tf.keras.layers.Attention layer for Luong attention, and an AdditiveAttention layer for Bahdanau attention.
# The Keras Attention and AdditiveAttention layers both expect a list as input, containing two or three items: the queries, the keys, and optionally the values. If you do not pass any values, then they are automatically equal to the keys.
attention_layer = tf.keras.layers.Attention()
# Next, we need to create the attention layer and pass it the decoder's states and the encoder’s outputs. 
# However, to access the decoder’s states at each step we would need to write a custom memory cell. 
# For simplicity, let’s use the decoder’s outputs instead of its states: in practice this works well too, and it’s much easier to code.
attention_outputs = attention_layer([decoder_outputs, encoder_outputs])
# Then we just pass the attention layer’s outputs directly to the output layer, as suggested in the Luong attention paper.
output_layer = tf.keras.layers.Dense(vocab_size, activation="softmax")
Y_proba = output_layer(attention_outputs)
# So, looking at the previous code example again, the decoder outputs are the queries, and the encoder outputs are both the keys and the values.(解码器输出为query，编码器输出为key和value。)
# For each decoder output (i.e., each query), the attention layer returns a weighted sum of the encoder outputs (i.e., the keys/values) that are most similar to the decoder output.(对于每个解码器输出，注意力层会返回与解码器输出最相似的编码器输出的加权和。)

model = tf.keras.Model(inputs=[encoder_inputs, decoder_inputs],
                       outputs=[Y_proba])
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
model.fit((X_train, X_train_dec), Y_train, epochs=10,
          validation_data=((X_valid, X_valid_dec), Y_valid))

# If you train this model, you will find that it now handles much longer sentences.
print(translate("I like soccer and also going to the beach"))
# 'me gusta el fútbol y también ir a la playa'
```

In short, the attention layer provides a way to focus the attention of the model on part of the inputs. But there’s another way to think of this layer: it acts as a differentiable memory retrieval mechanism.(简而言之，注意力层提供了一种将模型的注意力集中在部分输入上的方法。不过，我们还可以从另一个角度来理解这一层：它充当了一种可区分的记忆检索机制。)

However, the model does not have discrete tokens to represent the keys (like "subject" or "verb"); instead, it has vectorized representations of these concepts that it learned during training, so the query it will use for the lookup will not perfectly match any key in the dictionary.(该模型并没有离散的token来表示key（如主语或动词）；然而它在训练过程中学到这些概念的向量表示，因此query不会完全匹配字典中的key。)

The solution is to compute a similarity measure between the query and each key in the dictionary, and then use the softmax function to convert these similarity scores to weights that add up to 1. If the key that represents the verb is by far the most similar to the query, then that key’s weight will be close to 1.(解决方法是计算qurey与key之间的相似度，然后使用softmax函数将这些相似度得分转换为总和为1的权重。如果代表动词的key是迄今为止与query最相似的，那么该key的权重就会接近1。)

Next, the attention layer computes a weighted sum of the corresponding values: if the weight of the "verb" key is close to 1, then the weighted sum will be very close to the representation of the word "played".

## Attention Is All You Need: The Original Transformer Architecture

In short, the left part of Figure 16-8 is the encoder, and the right part is the decoder. Each embedding layer outputs a 3D tensor of shape [batch size, sequence length, embedding size]. After that, the tensors are gradually transformed as they flow through the transformer, but their shape remains the same.

Now let’s walk through Figure 16-8 in more detail:

- First, notice that both the encoder and the decoder contain modules that are stacked N times. In the paper, N = 6. The final outputs of the whole encoder stack are fed to the decoder at each of these N levels.(注意编码器和解码器都堆叠了N个模块，论文中N = 6。整个堆叠的编码器的输出最终被传入到堆叠N层的解码器。)
- Zooming in, you can see that you are already familiar with most components: there are two embedding layers; several skip connections, each of them followed by a layer normalization layer; several feedforward modules that are composed of two dense layers each (the first one using the ReLU activation function, the second with no activation function); and finally the output layer is a dense layer using the softmax activation function.
- The encoder's multi-head attention layer updates each word representation by attending to (i.e., paying attention to) all other words in the same sentence.(编码器的多头注意层会通过注意同一句子中的所有其他单词来更新每个单词的表征。)
- The decoder’s masked multi-head attention layer does the same thing, but when it processes a word, it doesn’t attend to words located after it: it’s a causal layer.(解码器的遮蔽多头注意层做着同样的事情，但是当它处理一个单词时，它不会注意位于该单词之后的单词：这是一个因果层。)
- The decoder’s upper multi-head attention layer is where the decoder pays attention to the words in the English sentence. This is called cross-attention, not self-attention in this case.(解码器的上多头注意层是解码器注意英语句子中单词的地方。)
- The positional encodings are dense vectors (much like word embeddings) that represent the position of each word in the sentence. The $n^{th}$ positional encoding is added to the word embedding of the $n^{th}$ word in each sentence. (位置编码是表示每个单词在句子中位置的密集向量。第n个位置编码被添加到每个句子中第n个单词的词嵌入中。)

**NOTE**: The first two arrows going into each multi-head attention layer in Figure 16-8 represent the keys and values, and the third arrow represents the queries. In the self-attention layers, all three are equal to the word representations output by the previous layer, while in the decoder’s upper attention layer, the keys and values are equal to the encoder’s final word representations, and the queries are equal to the word representations output by the previous layer.(图16-8中进入每个多头注意层的前两个箭头代表key和value，第三个箭头代表query。在自注意层中，这三个箭头都等于上一层输出的单词表示，而在解码器的上层注意层中，key和value等于编码器的最终单词表示，query等于上一层输出的单词表示。)

### Positional encodings

#### trainable positional encodings

A positional encoding is a dense vector that encodes the position of a word within a sentence: the $i^{th}$ positional encoding is added to the word embedding of the $i^{th}$ word in the sentence.(位置编码是一个密集向量，用于编码单词在句子中的位置：第i个位置编码被添加到句子中第i个单词的词嵌入中。)

```python
# The easiest way to implement positional encoding is to use an Embedding layer and make it encode all the positions from 0 to the maximum sequence length in the batch, then add the result to the word embeddings. The rules of broadcasting will ensure that the positional encodings get applied to every input sequence. (广播规则将确保位置编码应用于每个输入序列)
# For example, here is how to add positional encodings to the encoder and decoder inputs:
max_length = 50  # max length in the whole training set
embed_size = 128
# The encoder and the decoder share the same Embedding layer for the positional encodings, since they have the same embedding size.
pos_embed_layer = tf.keras.layers.Embedding(max_length, embed_size)
batch_max_len_enc = tf.shape(encoder_embeddings)[1]
encoder_in = encoder_embeddings + pos_embed_layer(tf.range(batch_max_len_enc))
batch_max_len_dec = tf.shape(decoder_embeddings)[1]
decoder_in = decoder_embeddings + pos_embed_layer(tf.range(batch_max_len_dec))
```

#### fixed positional encodings

Instead of using trainable positional encodings, the authors of the transformer paper chose to use fixed positional encodings, based on the sine and cosine functions at different frequencies.(作者没有使用可训练的位置编码，而是根据不同频率的正弦和余弦函数，选择使用固定位置编码。)

The positional encoding matrix P is defined in Equation 16-2 and represented at the top of Figure 16-9 (transposed), where $P_{p,i}$ is the $i_{th}$ component of the encoding for the word located at the $p_{th}$ position in the sentence.($P_{p,i}$是位于句子第p个位置的单词编码的第i个分量。)

$$
P_{p,i}=\begin{cases}
& \sin(p/10000^{i/d}) & \mathbf{if\ i\ is\ even} \\
& \cos(p/10000^{(i-1)/d}) & \mathbf{if\ i\ is\ odd}
\end{cases}
$$

This solution can give the same performance as trainable positional encodings, and it can extend to arbitrarily long sentences without adding any parameters to the model (however, when there is a large amount of pretraining data, trainable positional encodings are usually favored).

After these positional encodings are added to the word embeddings, the rest of the model has access to the absolute position of each word in the sentence because there is a unique positional encoding for each position (e.g., the positional encoding for the word located at the 22nd position in a sentence is represented by the vertical dashed line at the top left of Figure 16-9, and you can see that it is unique to that position).(将这些位置编码添加到单词嵌入中后，模型的其他部分就可以获得每个单词在句子中的绝对位置，因为每个位置都有唯一的位置编码，例如位于句子第22位置的单词的位置编码由图16-9左上方的垂直虚线表示，可以看出该位置的位置编码是唯一的。)

Moreover, the choice of oscillating functions (sine and cosine) makes it possible for the model to learn relative positions as well. For example, words located 38 words apart (e.g., at positions p = 22 and p = 60) always have the same positional encoding values in the encoding dimensions i = 100 and i = 101.(振荡函数的选择使模型可以学习相对位置。例如相距38个单词的单词（如位置p = 22和p = 60）在编码维度i = 100和i = 101中总是具有相同的位置编码值)

This explains why we need both the sine and the cosine for each frequency: if we only used the sine (the blue wave at i = 100), the model would not be able to distinguish positions p = 22 and p = 35 (marked by a cross).(这就解释了为什么我们需要频率不同的正弦波和余弦波：如果我们只使用正弦波，模型将无法区分p = 22和p = 35这两个位置)

```python
# For efficiency reasons, we precompute the positional encoding matrix in the constructor. 
# The call() method just truncates this encoding matrix to the max length of the input sequences, and it adds them to the inputs. 
# We also set supports_masking=True to propagate the input’s automatic mask to the next layer.
class PositionalEncoding(tf.keras.layers.Layer):
    def __init__(self, max_length, embed_size, dtype=tf.float32, **kwargs):
        super().__init__(dtype=dtype, **kwargs)
        assert embed_size % 2 == 0, "embed_size must be even"
        p, i = np.meshgrid(np.arange(max_length),
                           2 * np.arange(embed_size // 2))
        pos_emb = np.empty((1, max_length, embed_size))
        pos_emb[0, :, ::2] = np.sin(p / 10_000 ** (i / embed_size)).T
        pos_emb[0, :, 1::2] = np.cos(p / 10_000 ** (i / embed_size)).T
        self.pos_encodings = tf.constant(pos_emb.astype(self.dtype))
        self.supports_masking = True

    def call(self, inputs):
        batch_max_length = tf.shape(inputs)[1]
        return inputs + self.pos_encodings[:, :batch_max_length]

# Let’s use this layer to add the positional encoding to the encoder’s inputs:
pos_embed_layer = PositionalEncoding(max_length, embed_size)
encoder_in = pos_embed_layer(encoder_embeddings)
decoder_in = pos_embed_layer(decoder_embeddings)

# extra code – this cells generates and saves Figure 16–9
figure_max_length = 201
figure_embed_size = 512
pos_emb = PositionalEncoding(figure_max_length, figure_embed_size)
zeros = np.zeros((1, figure_max_length, figure_embed_size), np.float32)
P = pos_emb(zeros)[0].numpy()
i1, i2, crop_i = 100, 101, 150
p1, p2, p3 = 22, 60, 35
fig, (ax1, ax2) = plt.subplots(nrows=2, ncols=1, sharex=True, figsize=(9, 5))
ax1.plot([p1, p1], [-1, 1], "k--", label="$p = {}$".format(p1))
ax1.plot([p2, p2], [-1, 1], "k--", label="$p = {}$".format(p2), alpha=0.5)
ax1.plot(p3, P[p3, i1], "bx", label="$p = {}$".format(p3))
ax1.plot(P[:,i1], "b-", label="$i = {}$".format(i1))
ax1.plot(P[:,i2], "r-", label="$i = {}$".format(i2))
ax1.plot([p1, p2], [P[p1, i1], P[p2, i1]], "bo")
ax1.plot([p1, p2], [P[p1, i2], P[p2, i2]], "ro")
ax1.legend(loc="center right", fontsize=14, framealpha=0.95)
ax1.set_ylabel("$P_{(p,i)}$", rotation=0, fontsize=16)
ax1.grid(True, alpha=0.3)
ax1.hlines(0, 0, figure_max_length - 1, color="k", linewidth=1, alpha=0.3)
ax1.axis([0, figure_max_length - 1, -1, 1])
ax2.imshow(P.T[:crop_i], cmap="gray", interpolation="bilinear", aspect="auto")
ax2.hlines(i1, 0, figure_max_length - 1, color="b", linewidth=3)
cheat = 2  # need to raise the red line a bit, or else it hides the blue one
ax2.hlines(i2+cheat, 0, figure_max_length - 1, color="r", linewidth=3)
ax2.plot([p1, p1], [0, crop_i], "k--")
ax2.plot([p2, p2], [0, crop_i], "k--", alpha=0.5)
ax2.plot([p1, p2], [i2+cheat, i2+cheat], "ro")
ax2.plot([p1, p2], [i1, i1], "bo")
ax2.axis([0, figure_max_length - 1, 0, crop_i])
ax2.set_xlabel("$p$", fontsize=16)
ax2.set_ylabel("$i$", rotation=0, fontsize=16)
save_fig("positional_embedding_plot")
plt.show()
```

### Multi-head attention

To understand how a multi-head attention layer works, we must first understand the **scaled dot-product attention** layer, which it is based on. Its equation is shown in Equation 16-3, in a vectorized form.

$$
Attention(\mathbf{Q},\mathbf{K},\mathbf{V})=softmax(\frac{\mathbf{Q}\mathbf{K}^T}{\sqrt{d_{keys}}})\mathbf{V}
$$

- Q is a matrix containing one row per query. Its shape is $[n_{queries}, d_{keys}]$, where $n_{queries}$ is the number of queries and $d_{keys}$ is the number of dimensions of each query and each key.
- K is a matrix containing one row per key. Its shape is $[n_{keys}, d_{keys}]$, where $n_{keys}$ is the number of keys and values.
- V is a matrix containing one row per value. Its shape is $[n_{keys}, d_{values}]$, where $d_{values}$ is the number of dimensions of each value.
- The shape of $\mathbf{Q}\mathbf{K}^T$ is $[n_{queries}, n_{keys}]$: it contains one similarity score for each query/key pair. The output of the softmax function has the same shape, but all rows sum up to 1.
- The final output has a shape of $[n_{queries}, d_{values}]$: there is one row per query, where each row represents the query result (a weighted sum of the values).
- The scaling factor $\frac{1}{\sqrt{d_{keys}}}$ scales down the similarity scores to avoid saturating the softmax function, which would lead to tiny gradients.

```python
# We use a stack of two blocks (N=2) instead of six, since we don’t have a huge training set.
N = 2  # instead of 6
num_heads = 8
dropout_rate = 0.1
n_units = 128  # for the first Dense layer in each Feed Forward block
# We want to tell the MultiHeadAttention layer to ignore all the padding tokens in the values. 
# So, we first compute the padding mask using tf.math.not_equal(encoder_input_ids, 0). 
# This returns a Boolean tensor of shape [batch size, max sequence length].
# We then insert a second axis using [:, tf.newaxis], to get a mask of shape [batch size, 1, max sequence length].
encoder_pad_mask = tf.math.not_equal(encoder_input_ids, 0)[:, tf.newaxis]
Z = encoder_in
for _ in range(N):
    skip = Z
    # The MultiHeadAttention layer accepts an attention_mask argument, which is a Boolean tensor of shape [batch size, max query length, max value length]: 
    # for every token in every query sequence, this mask indicates which tokens in the corresponding value sequence should be attended to.
    attn_layer = tf.keras.layers.MultiHeadAttention(
        num_heads=num_heads, key_dim=embed_size, dropout=dropout_rate)
    Z = attn_layer(Z, value=Z, attention_mask=encoder_pad_mask)
    Z = tf.keras.layers.LayerNormalization()(tf.keras.layers.Add()([Z, skip]))
    skip = Z
    Z = tf.keras.layers.Dense(n_units, activation="relu")(Z)
    Z = tf.keras.layers.Dense(embed_size)(Z)
    Z = tf.keras.layers.Dropout(dropout_rate)(Z)
    Z = tf.keras.layers.LayerNormalization()(tf.keras.layers.Add()([Z, skip]))

# The first multi-head attention layer is a self-attention layer, like in the encoder, 
# but it is a masked multi-head attention layer, meaning it is causal: it should ignore all tokens in the future. 
# So, we need two masks: a padding mask and a causal mask. Let’s create them:
decoder_pad_mask = tf.math.not_equal(decoder_input_ids, 0)[:, tf.newaxis]
causal_mask = tf.linalg.band_part(  # creates a lower triangular matrix
    tf.ones((batch_max_len_dec, batch_max_len_dec), tf.bool), -1, 0)

encoder_outputs = Z  # let's save the encoder's final outputs
Z = decoder_in  # the decoder starts with its own inputs
for _ in range(N):
    skip = Z
    attn_layer = tf.keras.layers.MultiHeadAttention(
        num_heads=num_heads, key_dim=embed_size, dropout=dropout_rate)
    Z = attn_layer(Z, value=Z, attention_mask=causal_mask & decoder_pad_mask)
    Z = tf.keras.layers.LayerNormalization()(tf.keras.layers.Add()([Z, skip]))
    skip = Z
    attn_layer = tf.keras.layers.MultiHeadAttention(
        num_heads=num_heads, key_dim=embed_size, dropout=dropout_rate)
    Z = attn_layer(Z, value=encoder_outputs, attention_mask=encoder_pad_mask)
    Z = tf.keras.layers.LayerNormalization()(tf.keras.layers.Add()([Z, skip]))
    skip = Z
    Z = tf.keras.layers.Dense(n_units, activation="relu")(Z)
    Z = tf.keras.layers.Dense(embed_size)(Z)
    Z = tf.keras.layers.LayerNormalization()(tf.keras.layers.Add()([Z, skip]))

Y_proba = tf.keras.layers.Dense(vocab_size, activation="softmax")(Z)
model = tf.keras.Model(inputs=[encoder_inputs, decoder_inputs],
                       outputs=[Y_proba])
model.compile(loss="sparse_categorical_crossentropy", optimizer="nadam",
              metrics=["accuracy"])
model.fit((X_train, X_train_dec), Y_train, epochs=10,
          validation_data=((X_valid, X_valid_dec), Y_valid))

print(translate("I like soccer and also going to the beach"))
# 'me gusta el fútbol y yo también voy a la playa'
```