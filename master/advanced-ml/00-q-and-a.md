% Advanced Machine Learning Questions, 2021/2022
% 
%

# 1 partial exam

- **What has been enabled by Deep Learning?**

Representation learning.

- **Which of these statement is wrong?**

Factor of variations is directly observable

- **ADALINE**

Used continuos predicted values to learn

- **Which of this statements is correct?**

    - [ ] Deep learning is primally concerned with building more accurate models of how the brain actually works
    - [x] Neuroscience was the inspiring science for neural networks
    - [x] Connectionism arose in the context of cognitive science
    - [x] One key concept of connectionism is the distributed representation
    - [ ] In deep learning each concept is represented by one neuron
    - [ ] The backpropagation is based on the concept of semantic similarity

- **Which among this factors did enable Deep Learning?**

    - [x] Availability of large datasets
    - [ ] Network connectivity
    - [?] The implementation of backpropagation (la prof dice che è ambigua, potrebbe essere considerata vera)
    - [ ] Distributed representation
    - [x] Availability of faster CPUs

- **Algorithims for weight adjustement in a classification network are made to linearly separate the point belonging in the 2 classes**

False

- **Weight adjusstements are aimed at learning a good separation function**

True

- **Recurrent neural networks..**

Capture sequential information through loop connections

- **The behavior of intermediate layers in a FFN are simply specified by the training data**

False

- **Multilayer networks need to specify the kernel function**

False

- **Kernel functions first maps features in a different space and then evaluate the inner product**

False

- **In general, kernel machine suffer of high computational cost of training when the dataset is large**

True, because their complexity is linear with the number of training examples

- **Which of these sentences is true?**

    - [x] The gradient descent algorithm may not converge if the learning rate is too big.
    - [ ] The gradient descent algorithm may not converge if the learning rate is too small.
    - [ ] The gradient descent algorithm always converge to the global optimum
    - [x] The gradient descent algorithm can also be applied for solving maximization problems
    - [x] The gradient descent algorithm may converge to a local optimum

- **To apply an iterative numerical optimization procedure for learning the weight of a FFN**

    - [x] The cost function may be a function which we cannot evaluate analitically
    - [ ] We need to know the analitical form of the gradient
    - [x] It is enough to have some way of approximating the gradient

- **For training a multilayer NN**

    - [ ] We must adjust the weight of all the layers in one go
    - [ ] We train one layer at time using the error made by each layer in predicting the final result
    - [x] We train one layer at time using the error made in reproducing its own input

- **A SVM can be trained by solving a system of equations while a neural network can always be trained by using convex optimization**

Partially true

_First part is true, second part is false_