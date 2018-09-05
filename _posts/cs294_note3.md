# Reinforcement learning introduction

## Markov chain

![](img/posts/cs294_3/001.png)

$\hat{\mu_t}$ is a vector, and $\mu_{t,i}$ is the probability that you're in state $i$ at timestep $t$ .



## Markov Decision Process

![](img/posts/cs294_3/002.png)

## Partially Observed Markov Decision Process

![](img/posts/cs294_3/003.png)

## The goal of reinforcement learning

![](img/posts/cs294_3/004.png)

If we know the policy, we can easily turn our MDP to markov chain.

![](img/posts/cs294_3/005.png)

#### finite horizon case

![](img/posts/cs294_3/006.png)

The probability of $s_t$ and $a_t$ is the marginal distribution at timestep t in this Markov chain.

#### infinite horizon case

![](img/posts/cs294_3/007.png)

You can always find **a distribution that state$t$ and action$a$ will converge to**. So $p_\theta(s,a)$ accord with a stationary distribution. And as the timestep $T$ is infinity, if the Markov chain falls into the stationary distribution, and then stays there for infinitely long time, that sum is entirely dominated by the expectation under stationary distribution. But rarely exist reinforcement learning algorithms try to find $\mu$.

![](img/posts/cs294_3/008.png)

## Expectations is what we care about

![](img/posts/cs294_3/009.png)

In reinforcement learning, we always care about expectations not individual values and this is important because this gives us some good mathematics properties. If we drive a car to climb a mountain, and if we drive on the road, we get a reward +1, and if we drive off the cliff, we get a reward -1. And this reward function is not smooth. But if we abstract the probability of falling in this dynamic system, then the expectation of the reward under the stationary distribution with this probability$\sigh$ is actually smooth in $\sigh$. This is very important because **this is what allows us to use gradient based algorithms with reinforcement learning to optimize non-smooth objectives, include non-smooth dynamics or non-smooth reward or both.**

## Some algorithms

![](img/posts/cs294_3/010.png)

![](img/posts/cs294_3/011.png)

![](img/posts/cs294_3/012.png)

![](img/posts/cs294_3/013.png)

![](img/posts/cs294_3/014.png)

## Trade-off

![](img/posts/cs294_3/015.png)

The different between **on policy** and **off policy**

![](img/posts/cs294_3/016.png)

![](img/posts/cs294_3/017.png)

If you have very fast simulator, maybe you don't care about efficiency. Policy gradient algorithms even though they are on-policy, they are also often very easy to parallelize. And model-based RL algorithms always need to fit a lot of different neural network models.

![](img/posts/cs294_3/018.png)

![](img/posts/cs294_3/019.png)

![](img/posts/cs294_3/020.png)

## Examples of specific algorithms

![](img/posts/cs294_3/021.png)

