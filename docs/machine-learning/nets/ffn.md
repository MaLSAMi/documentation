### Feed Forward Network Documentation

This project attempted to train a feed forward network on taskset parameters to predict whether or not a taskset represents an executable combination of tasks.

In the end it is a four layers feed forward neural network with two hidden layers of size 50. The hidden layers each had leaky-RELU non-linearities. 

Although ReLU functions are very popular with most Feed-Forward Neural Networks. ReLU functions are popular because of their handling of the vanishing gradient that often arises from other activation functions. The advantage of Leaky ReLU is that it preserves more of the data than a regular ReLU function. While the ReLU chooses the max(0,input), the leaky-ReLU will choose: x for x &ge; 0 and otherwise &alpha; * x where &alpha; is an argument to the function, with a default value of 0.01.

The input dimension (N X D) constituted the number of tasksets (N) where each taskset contained a certain number of tasks. The parameters of these individual tasks within the taskset made up the parameters/features of the taskset itself. In our case D equals 12 for a taskset of size three. 

The output dimension (N X 2) is two neurons which each output a value between '1' and '0' using a sigmoid function. 

The final configuration of the network consists of the following:

- mini batch size: 30
- hidden layers: 2, both of size 50
- learning rate: 1e-5
- loss function: CrossEntropyLoss
- optimizer: Adam

The preprocessing of the data included the removal of parameters that were not unique, thus having no impact on the training, removing some tasksets, which have parameters that were thought to be outliers that distorted the normalized data followed, of course by normalizing the input values.
After about 200 epochs improvement starts to stagnate at an accuracy of about 70% if an error of up to 0.1 is allowed.
The next 950 epochs only show an improvement of another 4% on the same data.

The available data was split into 60% training, 20% validation and 20% test data.
Out of the 13 parameters per task only 4 were distinct. In the end only the priority, the argument, the period and the number of jobs were kept.

Previously to the work in this project a Bachelors Thesis tried to train a small feed forward network on a very limited dataset. The thesis only used a tasktype identifyer and the given critical time as inputs. The code is available [here](https://github.com/RobertHa/Bachelor-Thesis).
