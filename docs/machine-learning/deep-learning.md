### Deep Learning

The use of deep learning has pervaded aritificial intelligence and is being applied to virtually all projects. Deep Learning's strengths lie in its ability to pattern match data with complicated structures given that it has enough training data. Although deep learning seems to be the obvious answer with its advanced techniques, it is relatively heavyweight. Deep Learning works best when there is a lot of data to sample from and if possible, if we have an idea of what the data is like.  

There are virtually endless number of deep learning models that are possible to try out. We have listed a few of them below. 


### *[Feed Forward Neural Network](https://en.wikipedia.org/wiki/Feedforward_neural_network)*

A Feed-forward artificial neural network is a multilayer perceptron and is the most basic neural network available. A feed forward network is a necessary model and will act as the *control* network for the rest of the deep learning models. Feed Forward Networks are adaptable in fitting simple data. We hope to acheive as high of a possible of an accuracy on this type of network before venturing into the more advanced networks listed below. A simple Feed Forward Net has already been trained and fitted with some success (80% accuracy.)

An implementation for a basic Feed Forward Network already exists. The repo and expansive documentation is provided *[here](nets/ffn)*. 

### *[Recurrent Neural Networks](https://en.wikipedia.org/wiki/Recurrent_neural_network)* 

Recurrent Neural Networks are types of networks which utilizes 'memory'. These networks are very similiar to regular feed forward networks except for their ability to process previously analyzed along with the data that is currently being processed. These types of networks are especially beneficial for temporal and sequence analysis. This type of network could prove to be fruitful in the online learning phase as this network can better analyze recent events and use them in the learning process. At the same time, thie network will still be heavy duty and possibly computationally more expensive than the regular feed-forward network. 


#### *[Generative Adversarial Networks](https://en.wikipedia.org/wiki/Generative_adversarial_network)*

A GAN generally does not describe the structure of the neural network, but rather two types of neural networks which work together (or against each other). One generates data similar to some real dataset and the second network, which was formerly trained on the original dataset evaluates the generated data. The generator intends on "fooling" the evaluating network into classifying the generated data as real. While training, the generator becomes better at creating data close to the real dataset and the evaluating network becomes better at flagging faulty or erroneous data. 

We can think of the generator as producing the data and the discriminator as a regular supervised network that is no different from the others. The discriminator however can classify real and fake data more accurately. The generator produces samples to 'misclassify' the discriminator while the discriminator is training to counteract it.  

#### *[Convolutional Neural Networks](https://en.wikipedia.org/wiki/Convolutional_neural_network)*

A convolutional networks biggest strength is in its ability to extract the relevant features from an extremely large dataset. Convolutional networks are usually used in image processing as they are effective at processing images based on the information different areas of the image gives. Other than image processing, these types of networks are very good at measuring structured information. This includes text classificatoin and other problems in which the data's placement gives clues as to its meaning. If the data from the distributor happens to be structured in any way, the convolutional network has a good chance of performing well on it. 


### *[Spiking Neural Networks](https://en.wikipedia.org/wiki/Spiking_neural_network)*

Spiking Neural Networks refer to any network in which the input nodes(neurons) propogate the information at different times throughout the network. Each input neuron has an activation level in which incoming spikes determines pushes the function higher or lower. These networks most closely model real neurons in the brain, as all potential information is not fully processed at each time. The problem is that spiking is a noisy process, and may skew the data. The spikes are part of the learning process, and so the times the neurons are activated is analyzed just as much as what the neurons are sending. The idea of spiking can be applied to any of the other neural networks above, as it resembles more of a hyperparameter than an actual unique network model. A network using spiking is difficult to train as the signal nature of the spikes may be non-continuous and non-differentiable. 
