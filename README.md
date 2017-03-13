Read more about this from my website. https://bhaktipriya96.wordpress.com/generative-learning-blues-composer/

<span style="font-weight:400;">My deep interests in Music and Mathematics, lead me into building an AI Blues composer, that generates original Blues tunes using Restricted Boltzmann machines, Gibbs Sampling and a massive collection of popular Blues MIDI files. You can find the code [here](https://github.com/bhaktipriya/Blues).</span> <span style="font-weight:400;">Here's a closer look at the project:</span>

## Restricted Boltzmann machines:

A restricted Boltzmann machine (RBM) is a generative stochastic artificial neural network that can learn a probability distribution over its set of inputs. RBMs are by far the most basic NNs that I have come across. It's a shallow, two-layer neural net that constitutes the building blocks of the _deep-belief networks_. There are just 2 layers in an RBM viz the visible layer and the hidden layer. Forward pass of an RBM predicts the node activations ie..probability of output given a weighted x: `p(a|x; w)`. The backward pass of an RBM predicts the original data ie.. it tries to spit out the reconstructions. Given activation `a`,  it gives us probability of inputs `x`  which are weighted with the same coefficients as those used on the forward pass. Thus back propagation is nothing but `p(x|a; w)`. We exploit this reconstruction ability of the RBM, for generative learning. We supply it the a note and it generates the possible original output for the activation supplied. Essentially, we are trying to learn the music distribution of the Blues Genre. Together, we can obtain the joint probability distribution of inputs _x_ and activation _a ie.._ `p(x, a)`. ![reconstruction_rbm](https://bhaktipriya96.files.wordpress.com/2017/02/reconstruction_rbm.png)

## KL Divergence Algorithm:

To measure the distance between its estimated probability distribution and the ground-truth distribution of the input, RBMs use Kullback Leibler Divergence. ![kl_divergence_rbm](https://bhaktipriya96.files.wordpress.com/2017/02/kl_divergence_rbm.png)   Over the iterations, the weights of the RBMs are so adjusted such that the RBM learns to approximate the input distribution, which is encoded in the activations of the hidden layer. As the learning proceeds the 2 distributions converge. We use 2 tricks here to speed up the convergence process:

*   we initialize the Markov chain with a training example (so that it is close to the final distribution)
*   CD doesn't wait for the chain to converge. Samples are obtained after k-steps of Gibbs sampling. Typically, k=1 works reasonably well.

## Gibbs Sampling:

Gibbs sampling is an MCMC Method. It samples from a conditional distribution when other parameters are fixed. Here, <span class="c1">Gibbs sampler is used to approximate the distribution of the RBM(defined by W, bh, bv). </span>

## The Experiment:

Trained over the popular Blues Midi Files. Our note range spans between the lowest and the highest note on the piano roll.  . I trained my model for 200 epochs, with a batch size of 100\. I generated 10 snippets of music. Each time, I supplied a null vector and obtained a sequence which was 15 time steps long.  

## Hear It:

https://soundcloud.com/bhaktipriya-shridhar/generative-learning-blues-music   References: https://deeplearning4j.org/restrictedboltzmannmachine http://deeplearning.net/tutorial/rbm.html
