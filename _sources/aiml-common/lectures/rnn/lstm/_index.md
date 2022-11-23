# The Long Short-Term Memory (LSTM) Cell Architecture

In the simple RNN we have seen the problem of exploding or vanishing gradients when [the span of back-propagation is large](http://ai.dinfo.unifi.it/paolo//ps/tnn-94-gradient.pdf) (large $\tau$). Using the conceptual IIR filter, that ultimately _integrates_ the input signal, we have seen that in order to avoid an exploding or vanishing impulse response, we need to control $w$. This is exactly what is being done in evolutionary RNN architectures that we will treat in this section called _gated RNNs_. The best known gated RNN architecture is called the LSTM _cell_ and in this case the weight $w$ is not fixed but it is determined based on the input sequence _context_. The architecture is shown below. 

![lstm-cell](images/lstm-cell-2.png)
*LSTM architecture: It is divided into three areas: input (green), cell state (blue) and output (red). You can clearly see the outer ($\mathbf h_{t-1}$ )and the inner ($\mathbf s_{t-1}$) recurrence loops. The multipliers are Hadamard products aka they apply element-wise.*

Because we need to capture the input context that involve going back several time steps in the past, we introduce an _additional_ inner recurrence loop that is effectively a variable length internal to the cell memory - we call this the _cell state_.  We employ another hidden unit called the _forget gate_  to learn the input context and the forgetting factor (equivalent to the $w$ we have seen in the IIR filter) i.e. the extent that the cell forgets the previous hidden state. We employ a couple of other gates as well: the _input gate_ and the _output gate_ as shown in the diagram below. 

In the following we are describing what each component is doing. Notation wise:

1. We use two indices - $t$ for the unfolding sequence index and $i$ for the cell index $i$ of the LSTM layer. 
2. We also denote by $\mathbf A(i,:)$,  the i-th row of the matrix $\mathbf A$.  

Notice that if you make the output factors of input and output gates equal to 1.0 and the forgetting factor equal to 0.0, we are back to the simple RNN architecture. 

## Input Gate

The input gate _protects the cell state_ contents from perturbations by irrelevant to the context inputs. Quantitatively,  input gate calculates the factor,

$$g_t(i) =\sigma \Big( \mathbf W_g(i,:) \mathbf h_{t-1}^i + \mathbf U_g(i,:) \mathbf x_t^i + \mathbf b_g^i \Big) $$

The gate uses the sigmoid function to produce a factor between 0 and 1 for _each_ of the cells of the LSTM layer - each cell is indexed by $i$. This factor is applied to the $i$-th cell's input that is the combination of a function  of the previous hidden state represented by the dot product $\mathbf W_g(i,:) \mathbf h_{t-1}^i$  and a function of the current input, represented by the dot product $\mathbf U_g(i,:) \mathbf x_t^i$. 

## Output Gate

The output gate _protects the subsequent cells_ from perturbations by irrelevant to their context cell state. Quantitatively,

$$h_t^i = q_t^i \tanh(s_t^i)$$ 

where $q_t^i$ is the output factor

$$q_t{(i)} =\sigma \Big( \mathbf W_o(i,:) \mathbf h_{t-1}^i + \mathbf U_o(i,:) \mathbf x_t^i + \mathbf b_o^i \Big) $$

## The Cell State and the Forget Gate

This is the heart of the LSTM cell, the cell state is the new memory that is introduced by LSTM - all the earlier factors are used to preserve it as long as it is needed by the use case. 

$$s_t^i = f_t^i s_{t-1}^i + g_t^i \tanh \Big( \mathbf W(i,:) \mathbf h_{t-1}^i + \mathbf U(i,:) \mathbf x_t^i + \mathbf b^i \Big)$$

The parameters $\theta_{in} = \{  \mathbf W, \mathbf U, \mathbf b \}$  are the recurrent weights, input weights and bias respectively at the input of the i-th LSTM cell.
 
The forget gate calculates the forgetting factor,

$$f_t^i =\sigma \Big( \mathbf W_f(i,:) \mathbf h_{t-1}^i + \mathbf U_f(i,:) \mathbf x_t^i + \mathbf b_f^i \Big) $$

Similar to the input gate, this factor determines the amount of the earlier cell state that is needed to be preserved. 

Closing, you can expect backpropagation to work similarly to simple RNN case [albeit with more complicated expressions](https://christinakouridi.blog/2019/06/19/backpropagation-lstm/). In the LSTM workshop that follows you will have the opportunity to look at an LSTM training from scratch. 

Hyperparameter optimization for LSTMs is addressed more formally ["LSTM: A Search Space Odyssey"](https://arxiv.org/pdf/1503.04069v1.pdf)

## LSTM Workshop

Please go through [this](https://github.com/christinakouridi/scratchML/tree/master/LSTM) from scratch implementation of LSTM. Note that the notation is different than in these notes and follows [this well known blog post](https://colah.github.io/posts/2015-08-Understanding-LSTMs/).  

## Additional Resources

Additional tutorial resources on LSTMs can be found here:
1. [A Critical Review of Recurrent Neural Networks for Sequence Learning](https://arxiv.org/pdf/1506.00019.pdf)
2. [Understanding LSTMs](https://colah.github.io/posts/2015-08-Understanding-LSTMs) 
3. [Illustrated guide to LSTMs](https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21)
4. [Simplest possible LSTM explanation video](https://www.youtube.com/watch?v=WCUNPb-5EYI)
