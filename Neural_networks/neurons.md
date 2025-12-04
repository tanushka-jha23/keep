# Neurons and Neural Networks

# What are neural networks?
Neural network is a common term when you study something related to machine learning. If we seggregate the term and take it one-by-one, then neural means "*Neuron* and network means a *structure* or a *mesh*. Neural networks are basically a graph of neurons. Now, what do we mean by the neurons here?? Let's cover them in the next section.

## Neurons
You might have idea about the neuron cell, also known as the brain cells of our body. The name *Neuron* is derived from there. Neurons basically have dendrites, body and axon. The neurons which we are talking about also have multiple inputs which can be compared to dendrites.

### Features of neuron
Neurons have mainly 3 features:-
- Activation function
- An array/vector of weights (which is associated which inputs)
- Bias value

### How the output is calculated?
Neurons or nodes of the neural networks have an input array. The weights are associated with each input. The output of the node is calculated by-:

```
y = A(b + $\sigma wx$)
```
Here, y is the output, b is the bias, *x* is the array of inputs and *w* is the vector of weights that are associated with each input. As w and x are vectors, their dot product can also be taken directly.
Activation function can be any function which takes the value inside the parenthesis as its input and produce an output.
To understand it better, we can take Sigmoid function as our activation function along with 10 random inputs.
