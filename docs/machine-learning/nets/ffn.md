### Feed Forward Network Documentation

This was a four layers feed forward neural network with two hidden layers of arbitrary length. The hidden layers each had leaky-RELU non-linearities. 

The input dimension (N X D) constituted the number of tasksets (N) where each taskset contained a certain number of tasks. The parameters of these individual tasks within the taskset made up the parameters/features of the taskset itself. 

The output dimension (H2 X 1) was a single neuron which outputs a '1' or '0' using a sigmoid function. The code is available [here](https://github.com/RobertHa/Bachelor-Thesis). 

The user can determine how many hidden units he or she would like to use. He or she is also allowed to decide on the number of epochs and the learning rate. This gives the user a bit of flexibility in fitting the model to the task data. 

Although ReLU functions are very popular with most Feed-Forward Neural Networks. ReLU functions are popular because of their handling of the vanishing gradient that often arises from other activation functions. The advantage of Leaky ReLU is that it preserves more of the data than a regular ReLU function. While the ReLU chooses the max(0,input), the leaky-ReLU will choose:
