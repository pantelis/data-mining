---
title: Word2Vec Workshop
---

# Word2Vec Workshop

## Example

{{<hint info>}}
The following example is from [here](https://iksinc.online/tag/skip-gram-model/).
{{</hint>}}

Consider the training corpus having the following sentences:

“the dog saw a cat”, 

“the dog chased the cat”, 

“the cat climbed a tree”

In this corpus $V=8$ and we are interested in creating word embeddings of order $d=3$. The parameter matrices are randomly initialized as

$$W = \begin{bmatrix} 0.54 &  0.28 &  0.42\\\\0.84 &  0.00 &  0.12\\\\ 0.67 &  0.83 &  0.14\\\\0.58 &  0.89 &  0.21\\\\0.19 &  0.11 &  0.22\\\\0.98 &  0.81 &  0.17\\\\0.82 &  0.27 &  0.43\\\\0.94 &  0.82 &  0.34
\end{bmatrix}$$

$$ W^\prime = \begin{bmatrix}0.18 &  0.37 &  0.01 &  0.25 &  0.80 &  0.02 &  0.60 &  0.60\\\\0.11 &  0.38 &  0.04 &  0.89 &  0.98 &  0.06 &  0.89 &  0.58\\\\0.74 &  0.63 &  0.58 &  0.02 &  0.21 &  0.54 &  0.77 &  0.25
\end{bmatrix}$$


**Suppose we want the network to learn relationship between the words “cat” and “climbed”. That is, the network should show a high probability for “cat” when “climbed” is presented at the input of the network.** In word embedding terminology, the word “cat” is referred as the target word and the word “climbed” is referred as the context word. In this case, the input vector $\mathbf x_{t+1}  =  [0 0 0 1 0 0 0 0]^T$. Notice that only the 4th component of the vector is 1 - the input word “climbed” holds for example the 4th position in a sorted list of corpus words. Given that the target word is "cat", the target vector will be $\mathbf x_t = [0 1 0 0 0 0 0 0 ]^T$.

With the input vector representing “climbed”, the output at the hidden layer neurons can be computed as 

$$\mathbf z_t^T = \mathbf x_{t+j}^T \mathbf W = \begin{bmatrix}
  0.58 &  0.89 &  0.21
\end{bmatrix}, j=1$$

Carrying out similar manipulations for hidden to output layer, the activation vector for output layer neurons can be written as

$$\mathbf z^\prime_j = \mathbf z_t^T \mathbf W^\prime =\begin{bmatrix}
  0.35 &  0.69 &  0.16 &  0.94 &  1.38 &  0.18 &  1.30 &  0.91
\end{bmatrix}$$

Since the goal is produce probabilities for words in the output layer,  $p(w_{t+j} | w_t; \theta)$ to reflect their next word relationship with the context word at input, we need the sum of neuron outputs in the output layer to add to one. This can be achieved with the softmax

$$\hat{\mathbf y}_j = \mathtt{softmax}(\mathbf z^\prime_j), j=1$$

Thus, the probabilities for eight words in the corpus are:

$$\hat{\mathbf y} = \begin{bmatrix}
  0.35 &  \mathbf{0.69} &  0.16 &  0.94 &  1.38 &  0.18 &  1.30 &  0.91
\end{bmatrix}$$

The probability in bold is for the chosen target word 'cat'. Given the target vector [0 1 0 0 0 0 0 0 ], the error vector for the output layer is easily computed via CE loss. Once the loss is known, the weights in the matrices W can be updated using backpropagation. Thus, the training can proceed by presenting different context-target words pairs from the corpus. The context can be more than one word and in this case the loss is the average loss across all pairs. 


## From scratch

This [self-contained implementation](https://nathanrooy.github.io/posts/2018-03-22/word2vec-from-scratch-with-python-and-numpy) is instructive and you should [go through it](https://github.com/nathanrooy/word2vec-from-scratch-with-python/blob/master/word2vec.py) to understand the word2vec embedding. 

{{< details "Word2Vec" "..." >}}
```python
#   Nathan A. Rooy
#   Simple word2vec from scratch with Python
#   2018-FEB
#
import numpy as np
import re
from collections import defaultdict



class word2vec():
    def __init__ (self):
        self.n = settings['n']
        self.eta = settings['learning_rate']
        self.epochs = settings['epochs']
        self.window = settings['window_size']
        pass
    
    
    # GENERATE TRAINING DATA
    def generate_training_data(self, settings, corpus):

        # GENERATE WORD COUNTS
        word_counts = defaultdict(int)
        for row in corpus:
            for word in row:
                word_counts[word] += 1

        self.v_count = len(word_counts.keys())

        # GENERATE LOOKUP DICTIONARIES
        self.words_list = sorted(list(word_counts.keys()),reverse=False)
        self.word_index = dict((word, i) for i, word in enumerate(self.words_list))
        self.index_word = dict((i, word) for i, word in enumerate(self.words_list))

        training_data = []
        # CYCLE THROUGH EACH SENTENCE IN CORPUS
        for sentence in corpus:
            sent_len = len(sentence)

            # CYCLE THROUGH EACH WORD IN SENTENCE
            for i, word in enumerate(sentence):
                
                #w_target  = sentence[i]
                w_target = self.word2onehot(sentence[i])

                # CYCLE THROUGH CONTEXT WINDOW
                w_context = []
                for j in range(i-self.window, i+self.window+1):
                    if j!=i and j<=sent_len-1 and j>=0:
                        w_context.append(self.word2onehot(sentence[j]))
                training_data.append([w_target, w_context])
        return np.array(training_data)


    # SOFTMAX ACTIVATION FUNCTION
    def softmax(self, x):
        e_x = np.exp(x - np.max(x))
        return e_x / e_x.sum(axis=0)


    # CONVERT WORD TO ONE HOT ENCODING
    def word2onehot(self, word):
        word_vec = [0 for i in range(0, self.v_count)]
        word_index = self.word_index[word]
        word_vec[word_index] = 1
        return word_vec


    # FORWARD PASS
    def forward_pass(self, x):
        h = np.dot(self.w1.T, x)
        u = np.dot(self.w2.T, h)
        y_c = self.softmax(u)
        return y_c, h, u
                

    # BACKPROPAGATION
    def backprop(self, e, h, x):
        dl_dw2 = np.outer(h, e)  
        dl_dw1 = np.outer(x, np.dot(self.w2, e.T))

        # UPDATE WEIGHTS
        self.w1 = self.w1 - (self.eta * dl_dw1)
        self.w2 = self.w2 - (self.eta * dl_dw2)
        pass


    # TRAIN W2V model
    def train(self, training_data):
        # INITIALIZE WEIGHT MATRICES
        self.w1 = np.random.uniform(-0.8, 0.8, (self.v_count, self.n))     # embedding matrix
        self.w2 = np.random.uniform(-0.8, 0.8, (self.n, self.v_count))     # context matrix
        
        # CYCLE THROUGH EACH EPOCH
        for i in range(0, self.epochs):

            self.loss = 0

            # CYCLE THROUGH EACH TRAINING SAMPLE
            for w_t, w_c in training_data:

                # FORWARD PASS
                y_pred, h, u = self.forward_pass(w_t)
                
                # CALCULATE ERROR
                EI = np.sum([np.subtract(y_pred, word) for word in w_c], axis=0)

                # BACKPROPAGATION
                self.backprop(EI, h, w_t)

                # CALCULATE LOSS
                self.loss += -np.sum([u[word.index(1)] for word in w_c]) + len(w_c) * np.log(np.sum(np.exp(u)))
                #self.loss += -2*np.log(len(w_c)) -np.sum([u[word.index(1)] for word in w_c]) + (len(w_c) * np.log(np.sum(np.exp(u))))
                
            print 'EPOCH:',i, 'LOSS:', self.loss
        pass


    # input a word, returns a vector (if available)
    def word_vec(self, word):
        w_index = self.word_index[word]
        v_w = self.w1[w_index]
        return v_w


    # input a vector, returns nearest word(s)
    def vec_sim(self, vec, top_n):

        # CYCLE THROUGH VOCAB
        word_sim = {}
        for i in range(self.v_count):
            v_w2 = self.w1[i]
            theta_num = np.dot(vec, v_w2)
            theta_den = np.linalg.norm(vec) * np.linalg.norm(v_w2)
            theta = theta_num / theta_den

            word = self.index_word[i]
            word_sim[word] = theta

        words_sorted = sorted(word_sim.items(), key=lambda(word, sim):sim, reverse=True)

        for word, sim in words_sorted[:top_n]:
            print word, sim
            
        pass

    # input word, returns top [n] most similar words
    def word_sim(self, word, top_n):
        
        w1_index = self.word_index[word]
        v_w1 = self.w1[w1_index]

        # CYCLE THROUGH VOCAB
        word_sim = {}
        for i in range(self.v_count):
            v_w2 = self.w1[i]
            theta_num = np.dot(v_w1, v_w2)
            theta_den = np.linalg.norm(v_w1) * np.linalg.norm(v_w2)
            theta = theta_num / theta_den

            word = self.index_word[i]
            word_sim[word] = theta

        words_sorted = sorted(word_sim.items(), key=lambda(word, sim):sim, reverse=True)

        for word, sim in words_sorted[:top_n]:
            print word, sim
            
        pass

#--- EXAMPLE RUN --------------------------------------------------------------+

settings = {}
settings['n'] = 5                   # dimension of word embeddings
settings['window_size'] = 2         # context window +/- center word
settings['min_count'] = 0           # minimum word count
settings['epochs'] = 5000           # number of training epochs
settings['neg_samp'] = 10           # number of negative words to use during training
settings['learning_rate'] = 0.01    # learning rate
np.random.seed(0)                   # set the seed for reproducibility

corpus = [['the','quick','brown','fox','jumped','over','the','lazy','dog']]

# INITIALIZE W2V MODEL
w2v = word2vec()

# generate training data
training_data = w2v.generate_training_data(settings, corpus)

# train word2vec model
w2v.train(training_data)

#--- END ----------------------------------------------------------------------+
```
{{</details>}}

## Tensorflow tutorial notebook

<iframe src="https://nbviewer.jupyter.org/github/tensorflow/docs/blob/master/site/en/tutorials/text/word2vec.ipynb" width="900" height="1200"></iframe>

 