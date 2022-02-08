---
title: REINFORCE
weight: 106
draft: false
---

# The REINFORCE Algorithm

Given that RL can be posed as an MDP, in this section we continue with a policy-based algorithm that learns the policy _directly_ by optimizing the objective function and can then map the states to actions.  The algorithm we treat here, called REINFORCE, is important although more modern algorithms do perform better. 

It took its name from the fact that during _training_ actions that resulted in good outcomes should become more probable—these actions are positively _reinforced_. Conversely, actions which resulted in bad outcomes should become less probable. If learning is successful, over the course of many iterations, action probabilities produced by the policy, shift to a distribution that results in good performance in an environment. Action probabilities are changed by following the policy gradient, therefore REINFORCE is known as a _policy gradient_ algorithm.
 
 The algorithm needs three components:

| Component                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Parametrized policy $\pi_\theta (a\|s)$           | The key idea of the algorithm is to learn a good policy, and this means doing function approximation. Neural networks are powerful and flexible function approximators, so we can represent a policy using a deep neural network (DNN) consisting of learnable parameters $\mathbf \theta$. This is often referred to as a policy network $\pi_θ$. We say that the policy is parametrized by  $\theta$. Each specific set of values of the parameters of the policy network represents a particular policy. To see why, consider $θ_1 ≠ θ_2$. For any given state $s$, different policy networks may output different sets of action probabilities, that is, $\pi_{θ_1}(a \| s) \neq \pi_{θ_2}(a \| s)$. The mappings from states to action probabilities are different so we say that $π_{θ_1}$ and $π_{θ_2}$ are different policies. A single DNN is therefore capable of representing many different policies. |
| The objective to be maximized $J(\pi_\theta)$[^1] | At this point is nothing else other than the expected discounted _return_ over policy, just like in MDP.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Policy Gradient                                   | A method for updating the policy parameters $\theta$. The policy gradient algorithm searches for a local maximum in $J(\pi_\theta)$:  $\max_\theta J(\pi_\theta)$. This is the common gradient ascent algorithm that we met in a similar form in neural networks. $$\theta ← \theta + \alpha \nabla_\theta J(\pi_\theta)$$ where $\alpha$ is the learning rate.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

Out of the three components, the most complicated one is the policy gradient that can be shown to be given by the differentiable quantity: 

$$ \nabla_\theta J(\pi_\theta)= \mathbb{E}_{\pi_\theta} \left[ \nabla_\theta \log \pi_\theta (a|s) v_\pi (s) \right ]$$

We understand that this expression came out of nowhere but the interested reader can find its detailed derivation in the chapter 2 of [this](https://www.amazon.com/Deep-Reinforcement-Learning-Python-Hands/dp/0135172381) reference. We can approximate the value at state $s$ with the return over many sample trajectories $\tau$ that are sampled from the policy network. 

$$ \nabla_\theta J(\pi_\theta)= \mathbb{E}_{\tau \sim \pi_\theta} \left[ G_t \nabla_\theta \log \pi_\theta (a|s) \right ]$$

where $G_t$ is the _return_ - a quantity we have seen earlier albeit now the return is limited by the length of each trajectory just like in MC method,

$$G_t(\tau) = \sum_{k=0}^{T-1}\gamma^k R_{t+1+k}$$

The $\gamma$ is usually a hyper-parameter that we need to optimize usually iterating over many values in [0.01,...,0.99] and selecting the one with the best results. 

We also have an expectation in the gradient expression that we need to address.  The expectation $\mathbb E_{\tau \sim \pi_\theta}$ we need to take is approximated with a summation over _each_ trajectory aka a Monte-Carlo approximation. Effectively, we are generating the right hand side as in line 8 in the code below, by sampling a trajectory (line 4) and estimating its return (line 7) in a completely model-free fashion i.e. without assuming any knowledge of the transition and reward functions. This is implemented next:

1: Initialize learning rate $\alpha$

2: Initialize weights θ of a policy network $π_θ$

3: for episode = 0, . . . , MAX_EPISODE do

4: &ensp;&ensp;Sample a trajectory using the policy network $\pi_\theta$, $τ = s_0, a_0, r_0, . . . , s_T, a_T, r_T$

5: &ensp;&ensp;Set $∇_θ J(π_θ) = 0$

6: &ensp;&ensp; for t = 0, . . . , T-1 do

7: &ensp;&ensp; &ensp;&ensp;         Calculate $G_t(τ)$

8: &ensp;&ensp; &ensp;&ensp;         $\nabla_\theta J(\pi_\theta) = \nabla_\theta J(\pi_\theta) + G_t (τ) \nabla_\theta \log \pi_\theta (a_t|s_t) $

9: &ensp;&ensp;     end for

10:&ensp;&ensp;      $θ = θ + α ∇_θ J(π_θ)$

11: end for

It is important that a trajectory is discarded after each parameter update—it cannot be reused. This is because REINFORCE is an _on-policy_ algorithm just like the MC it "learns on the job". This is evidently seen in line 10 where the parameter update equation uses the policy gradient that itself (line 8) directly depends on action probabilities $π_θ(a_t | s_t)$ generated by the _current_ policy $π_θ$ only and not some past policy $π_{θ′}$. Correspondingly, the return $G_t(τ)$ where $τ ~ π_θ$ must also be generated from $π_θ$, otherwise the action probabilities will be adjusted based on returns that the policy wouldn’t have generated.

### Policy Network

One of the key ingredients that REINFORCE introduces is the policy network that is approximated with a DNN eg. a fully connected neural network with a number of hidden layers that is hyper-parameter (e.g. 2 RELU layers). 

1: Given a policy network ``net``, a ``Categorical`` (multinomial) distribution class, and a ``state``

2: Compute the output ``pdparams = net(state)``

3: Construct an instance of an action probability distribution  ``pd = Categorical(logits=pdparams)``

4: Use pd to sample an action, ``action = pd.sample()``

5: Use pd and action to compute the action log probability, ``log_prob = pd.log_prob(action)``

Other discrete distributions can be used and many actual libraries parametrize continuous distributions such as Gaussians. 

## Applying the REINFORCE algorithm

It is now instructive to see an stand-alone example in python for the so called ``CartPole-v0`` [^2]

![cartpole](images/cartpole.png)

{{<details "REINFORCE Python Code" >}}
```python
 1  from torch.distributions import Categorical
 2  import gym
 3  import numpy as np
 4  import torch
 5  import torch.nn as nn
 6  import torch.optim as optim
 7
 8  gamma = 0.99
 9
10  class Pi(nn.Module):
11      def __init__(self, in_dim, out_dim):
12          super(Pi, self).__init__()
13          layers = [
14              nn.Linear(in_dim, 64),
15              nn.ReLU(),
16              nn.Linear(64, out_dim),
17          ]
18          self.model = nn.Sequential(*layers)
19          self.onpolicy_reset()
20          self.train() # set training mode
21
22      def onpolicy_reset(self):
23          self.log_probs = []
24          self.rewards = []
25
26      def forward(self, x):
27          pdparam = self.model(x)
28          return pdparam
29
30      def act(self, state):
31          x = torch.from_numpy(state.astype(np.float32)) # to tensor
32          pdparam = self.forward(x) # forward pass
33          pd = Categorical(logits=pdparam) # probability distribution
34          action = pd.sample() # pi(a|s) in action via pd
35          log_prob = pd.log_prob(action) # log_prob of pi(a|s)
36          self.log_probs.append(log_prob) # store for training
37          return action.item()
38
39  def train(pi, optimizer):
40      # Inner gradient-ascent loop of REINFORCE algorithm
41      T = len(pi.rewards)
42      rets = np.empty(T, dtype=np.float32) # the returns
43      future_ret = 0.0
44      # compute the returns efficiently
45      for t in reversed(range(T)):
46          future_ret = pi.rewards[t] + gamma * future_ret
47          rets[t] = future_ret
48      rets = torch.tensor(rets)
49      log_probs = torch.stack(pi.log_probs)
50      loss = - log_probs * rets # gradient term; Negative for maximizing
51      loss = torch.sum(loss)
52      optimizer.zero_grad()
53      loss.backward() # backpropagate, compute gradients
54      optimizer.step() # gradient-ascent, update the weights
55      return loss
56
57  def main():
58      env = gym.make('CartPole-v0')
59      in_dim = env.observation_space.shape[0] # 4
60      out_dim = env.action_space.n # 2
61      pi = Pi(in_dim, out_dim) # policy pi_theta for REINFORCE
62      optimizer = optim.Adam(pi.parameters(), lr=0.01)
63      for epi in range(300):
64          state = env.reset()
65          for t in range(200): # cartpole max timestep is 200
66              action = pi.act(state)
67              state, reward, done, _ = env.step(action)
68              pi.rewards.append(reward)
69              env.render()
70              if done:
71                  break
72          loss = train(pi, optimizer) # train per episode
73          total_reward = sum(pi.rewards)
74          solved = total_reward > 195.0
75          pi.onpolicy_reset() # onpolicy: clear memory after training
76          print(f'Episode {epi}, loss: {loss}, \
77          total_reward: {total_reward}, solved: {solved}')
78
79  if __name__ == '__main__':
80      main()
```
{{</details>}}

The REINFORCE algorithm presented here can generally be applied to continuous and discreet problems but it has been shown to possess high variance and sample-inefficiency. Several improvements have been proposed and the interested reader can refer to section 2.5.1 of the suggested book. 

[^1]: Notation wise, since we need to have a bit more flexibility in RL problems, we will use the symbol $J(\pi_\theta)$ as the objective function.
[^2]: Please note that SLM-Lab, the library that accompanies the suggested in the syllabus book, is a mature library and probably a good example of how to develop ML/RL libraries in python. You will learn a lot by reviewing the implementations under the ``agents/algorithms`` directory to get a feel of how RL problems are abstracted .  

