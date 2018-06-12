### Feed Forward Network Documentation

This was a five layers feed forward neural network with two hidden layers of arbitrary length. The hidden layers each had leaky-RELU non-linearities. 

The input dimension (N X D) constituted the number of tasksets (N) where each taskset contained a certain number of tasks. The parameters of these individual tasks within the taskset made up the parameters/features of the taskset itself. 

The output dimension (H2 X 1) was a single neuron which outputs a '1' or '0' using a sigmoid function. The code is available [here](https://github.com/RobertHa/Bachelor-Thesis). 

The user can determine how many hidden units he or she would like to use. He or she is also allowed to decide on the number of epochs and the learning rate. This gives the user a bit of flexibility in fitting the model to the task data. 