% Advanced Machine Learning Q&A, 2021/2022
% 
%

# 1 partial exam

- **Which of these AI systems is based on hard-coded rules?**
    
    - [x] Deep blue
    - [ ] AlphaGo
    - [ ] ADALINE

- **What has been enabled by Deep Learning?**

    - [ ] Multi-layer models
    - [ ] Automatic mapping between input and output
    - [x] Representation learning

- **Which of these statement is wrong?**

    - [ ] Many factors of variation influence every single piece of data
    - [x] Factor of variations is directly observable
    - [ ] Factor of variation can correspond to abstract features

- **ADALINE**

    - [x] Used continuos predicted values to learn
    - [ ] was a non-linear model
    - [ ] had weights that needed to be setted by an operator

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

    - [ ] in RNN the information flow only moves in one direction
    - [ ] are suitable for learning patterns in image data
    - [x] capture sequential information through loop connections

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

- **A neural network can be trained by solving a system of equations**

False

- **Sparse representations seem to be more beneficial than dense representations**

True

**In a neural network the nonlinearity causes the most interesting loss function to become non convex**

True

- **The loss function produces a numerical score that also depends on the set of the parameters which characterizes the FFN model**

True

- **The gradient can be estimated using a sample of training examples because is an expectation**

True

- **Regularization functions are added to the loss function to reduce their training error**

False

- **The sigmoid function**

    - [x] saturates for large argument values
    - [x] has a sensitive gradient when z is close to zero
    - [ ] has a zero gradient when the argument is close to zero
    - [ ] has a large gradient when it reaches saturation
    - [x] is 0 for LARGE negative argument values
    - [ ] in some cases it can produce a sparse network (many zero weights) that may be useful

- **Rectified linear unit (ReLU) is proposed to speed up the learning convergence**

True

- **Advantages of the ReLU functions are**

    - [x] ReLUs are much simpler computationally
    - [x] Reduced likelihood of the gradient to vanish
    - [x] The gradient is constant for z>0
    - [ ] Differentiability

2nd answer is true only for values >0

- **Leaky ReLUs**

    - [ ] saturate when the input is less than 0
    - [ ] need to perform exponential operations
    - [x] tend to blow up activation with the output range of [0, inf]

- **Maxout**

    - [x] has as spacial cases ReLU and Leaky ReLU
    - [ ] requires less parameters to be learned
    - [x] does not have the problem of saturation
    - [x] can approximate any convex function

- **Weights in a network must be initialized**

    - [ ] at zero
    - [ ] by mantaining symmetry
    - [ ] with zero variance
    - [x] randomly
    - [ ] it is indifferent

- **Which of the following statements are true?**

    - [x] When using SGD with mini-batches the model updates do not depend on the number of training examples
    - [ ] When using SGD with mini-batches the number of updates to reach convergence does not depend on the number of training examples
    - [ ] Once the SGD converges it is still useful to add more training examples sampled randomly
    - [x] For FNN it is important to initialize all weights to small random values
    - [x] The choice of cost functions is tightly coupled with the choice of the output unit

- **The function max{0, min{1, Wh + b}} is a good choice as an output function for classification problems**

    - [ ] No because it does not return a value between 0 and 1
    - [ ] Yes, because it returns a value between 0 and 1
    - [ ] Yes, because it is linear
    - [x] No, because it is not good for training

- **Softmax function**

    - [x] is a good choice for representing discrete probability distributions with n possible values
    - [x] it is a good output function because it is continuos and differentiable
    - [ ] since its output is a probability distribution it can always be interpreted as a confidence level
    - [ ] if the prediction is correct the penality is always 0

- **A Gaussian mixture output function**

    - [x] can represent multimodal functions
    - [ ] the weight associated to a gaussian in the mixture represents the probabilty of the output
    - [x] Mixtures are particularly suitable for generative models for speech or for movements of objects

- **Regularization**

    - [x] it reduces the validation/test error at the expenses of (acceptable) training error
    - [ ] enables the model to reach a point that does minimize the loss function
    - [ ] it enables the model to reduce the variability of the data

- **Which of this sentences are true?**

    - [x] Simpler models generalize better
    - [x] Multiple hypotesis (ensamble) models generalize better
    - [ ] More complex models can represent the true data generating process
    - [x] In general, when building machine learning models, the data generating process is not known.

- **Regularizing estimators**

    - [ ] Reduce bias
    - [x] Reduce the gap between training error and validation error
    - [ ] Reduce underfitting problems
    - [x] Can reduce the complexity of the model

- **Which of these sentences are false?**

    - [ ] if the weight of the regularization term in the loss function is too high it may imply underfitting
    - [x] if the weight of the penalization term in the loss function is too high it may imply overfitting
    - [ ] Regularizing the bias parameters can introduce a significan amount of underfitting
    - [x] Regularizing the bias parameters can introduce a significan amount of overfitting
    - [ ] Usually the bias parameters are not constrained by regularizing constraints

- **Parameter norm penalities**

    - [x] make the network more stable
    - [ ] minor variation or statistical noise on the inputs will result in large differences in the output
    - [x] encourage the network toward using small weights

- **Consider norm penalizations**

    - [x] Sum of absolute weights penalizes small weights more
    - [x] Squared weights penalizes large values more
    - [ ] L2 results in more sparse weights than L1
    - [ ] the addition of the L2 term modifies the learning rule by shrinking the weight factor by a costant factor on each parameter update
    - [x] L2 rescales the weights along the axes defined by the eigenvecotrs of the Hessian matrix

The 4th answer could be true if we interpret "constant" as proportional to the weight, but the proportionality is constant.

- **Which of these sentences are true?**
    
    - [x] Regularizing operators can be seen as soft costraints of the learning optimization problem
    - [ ] Regularizing operators can be done by optimizing with respect to the loss function and then re-projectng the solution in the feasible region $(k\Omega(\theta)) < 0$
    - [x] Explicit constraints implemented by re-projection do not necessarly encourage the weights to approach the origin
    - [x] Explicit constraints implemented by re-projection only have an effect when the weights become large and attempt to leave the constraint region.

- **Dataset augmentation**
    
    - [x] creates fake data and adds it to the training set
    - [ ] it is very effective for non supervised tasks
    - [x] Injecting noise in the input to a neural network can also be seen as a form of data augmentation

- **Which of these sentences is true?**
 
    - [ ] label smoothing is used for solving regression tasks
    - [x] label smoothing makes models robust to possible errors in the training set
    - [x] label smoothing can help convergence of maximum likelihoo learning with a softmax classifier and hard targets

- **Which of these sentences is false?**

    - [ ] Multitask forces to share a set of parameters across different tasks
    - [x] Multitask improves generalization when tasks are very different

- **Which of the following sentences are true?**

    - [ ] Parameter tying impose to a subset of parameters to be equal 
    - [x] Early stopping is a form of regularization
    - [x] Bagging is a form of ensemble model
    - [ ] Bagging is more effective if the output of the models learned are correlated
    - [x] Dropout is generally coupled with mini-batch based learning algotithm

- **In machine learning the cost function to minimize during the training process is the performance measure P representing the number of correct classifications on the test set**

False

- **The final aim of Machine Learning is**

    - [x] the miminization of the true risk function
    - [ ] the minimization of the empirical risk using a surrogate loss function

- **A surrogate loss function**

    - [ ] acts as a proxy to the true risk being "nice" enough to be optimized efficiently
    - [x] acts as a proxy to empirical risk being "nice" enough to be optimized effieciently

- **Early stopping halt criterion**

    - [x] is typically based on the performance obtained on a validation set
    - [ ] is typically based on the performance obtained on the training set

- **The accuracy of the estimated mean of the gradient**

    - [ ] it does not depend on the number of samples used
    - [ ] has a standard error which decreases linearly with the number of samples used
    - [x] it also depend on redundancies in sample data

2nd answer is false because the error decreses with square root trend

- **Ill conditioning of the Hessian matrix of the cost function**

    - [x] can be partly overcome by using the momentum strategy
    - [x] can prevent the gradient to arrive to a critical point
    - [x] can imply the very small steps are needed to decrease the cost function

The third answer is ambiguous (as usual). Prof says it's true anyway.

- **Local minima in deep learning problems**

    - [ ] are rare
    - [ ] are more common than saddle points
    - [x] are much more likely to have a low cost than a high cost

- **Neural networks with many layers**

    - [x] often have extremely steep regions (cliffs)
    - [x] often have flat regions
    - [x] often have many local minima of similar cost

- **Momentum update rule**
    
    - [ ] accumulates previous values of the cost function
    - [x] can be incorporated in SGD
    - [x] its step size is larger if previous gradients point in the same direction

- **AdaGrad algorithm**

    - [x] takes into account previous squared gradients
    - [x] decreases the learning rate too much in the early stages
    - [ ] it uses the same learning rate for all parameters

- **RMSProp**

    - [x] it takes into account the square gradients
    - [x] it is a modification of the AdaGrad algorithm
    - [ ] it does not require hyperparamters

- **Adam algorithm**

    - [ ] it also takes into account the curvature of the cost function through the second order derivatives
    - [x] it uses the momentum strategy
    - [x] it is based on RMSProp

- **A good initialization procedure**

    - [ ] assignes large weights
    - [ ] assignes extremely small weights
    - [x] none of the two

- **In initialization**

    - [x] larger weights break symmetry more
    - [ ] smaller weights propagate information more efficiently
    - [ ] large weights make the model more likely to reach solutions with good generalization property
    - [x] small weights make the model more robust

# 2 partial exam

- **Convolution is**

    - [ ] local in space, local in depth
    - [x] local in space, full in depth
    - [ ] full in space, local in depth
    - [ ] full in space, full in depth

- **Given the input volume with size H * W * K and a filter bank with size h * w * k we want to convolve them. The size of the output volume will be:**

    - [ ] H  * W * K
    - [ ] h * w * k
    - [ ] (H - h + 1) * (W - w + 1) * k
    - [ ] (H - h - 1) * (W - w - 1) * k
    - [x] (H - h + 1) * (W - w + 1) * 1
    - [ ] (H - h - 1) * (W - w - 1) * 1

- **How many channels (i.e. depth size) will have the output volume resulting from the convolution of an input volume with 16 channels (i.e. depth=16) with a filter bank of 16 filters?**

    - [ ] 1
    - [x] 16
    - [ ] 32

- **Given the input and the filter compute the convolution**

- **Compute the output after the applicationof max-pooling with neighborhood of size = 2 and stride = 2 to the input volume**

- **Which are common techniques to reduce overfitting?**

    - [x] Weight decay
    - [ ] Local response normalization
    - [x] Data augmentation
    - [ ] Data normalization
    - [x] Dropout

- **In data augmentation we have seen different policies (e.g. cropping, rotation, color cast, vignetting...)**

    - [ ] All policies are safe to use to any problem
    - [x] Only a subset of policies is safe to be used for each problem

- **We can diagnose the training and understand if we are overfitting:**

    - [ ] By plotting the loss on the training set across epochs
    - [ ] By plotting the loss on the validation set across epochs
    - [ ] By plotting the loss on the test set across epochs
    - [x] By plotting the accuracy on the training and validation sets across epochs

- **We can continue adding layers to a NN and we will continue to obtain better results**

    - [ ] Yes
    - [x] No

- **GoogLeNet (i.e. Inception-v1) introduced the use of auxiliary classifiers:**

    - [x] To mitigate the problem of vanishing gradients
    - [ ] To perform multi-task classification
    - [ ] To reduce overfitting

- **ResNets were able to train a model with 150+ layers by:**

    - [ ] Using just one fully-connected layer
    - [x] Introducing the residual connections
    - [ ] Using just 3x3 convolutional filters

- **If we have few data:**
    - [ ] We cannot use Deep Learning
    - [x] We can still use deep learning

- **From which layer we can extract activations to be used as features to classify data for a new small dataset that is similar to the dataset used to pre-train the whole network?**

    - [ ] Conv1
    - [ ] Conv2
    - [ ] Conv3
    - [ ] Conv4
    - [ ] Conv5
    - [x] FC6
    - [x] FC7
    - [ ] FC8

- **Model compression is only used to allow models to run on mobile devices**:

    - [ ] True
    - [x] False

- **Which is not a model compression technique?**
    
    - [ ] Weight sharing
    - [ ] Network pruning
    - [ ] Low rank matrix decomposition
    - [x] Dropout
    - [ ] Knowledge distillation
    - [ ] Quantization

- **Magnitude weight pruning removes the weights having:**
    
    - [ ] The lowest value
    - [x] The lowest absolute value
    - [ ] The highest absolute value
    - [ ] The highest value

- **Structured pruning**

    - [x] Aims to preserve network density for computational efficiency
    - [ ] Aims to increse network sparsity for computational efficiency

- **Low rank matrix decomposition is particularly useful in:**

    - [ ] Convolutional layers
    - [ ] Pooling layers
    - [x] Fully connected layers

- **RNNs are a family of neural networks for processing sequential data:**

    - [x] True
    - [ ] False

- **The computation in most RNNs can be decomposed in 3 blocks of parameters and associated transformations**:

    - [x] From the input to the hidden state
    - [ ] From the hidden state to the input
    - [x] From the previous hidden state to the next hidden state
    - [ ] From the next hidden state to the previous hidden state
    - [x] From the hidden state to the output
    - [ ] From the output to the hidden state

- **What is the name of the algorithm used to train RNNs?**
    
    - [ ] Backpropagation
    - [ ] Backpropagation through recurrency
    - [x] Backpropagation through time

- **Vanishing gradients are more easy to identify than exploding gradients**

    - [ ] True
    - [x] False

- **Exploding gradients are more difficult to handle than vanishing gradients**

    - [ ] True
    - [x] False

- **Vanishing gradients**

    - [x] Bias the parameters to capture short-term dependencies
    - [ ] Bias the parameters to capture long-term dependencies

- **Gated RNNs are based on the idea of creating paths throught time that have derivatives that neither vanish nor explode**

    - [x] True
    - [ ] False

- **LSTMs have the following gates:**

    - [x] Input gate
    - [ ] Remember gate
    - [ ] Recurrent gate
    - [x] Forget gate
    - [x] Output gate
    - [ ] Hidden gate

- **GRUs have**

    - [x] significally less parameters than LSTMs
    - [ ] significally more parameters than LSTMs

- **Federated learning aims to:**

    - [x] Collaboratevly train a ML model
    - [ ] Indipendently train a ML model

- **In federated learning, the data**

    - [ ] is shared across parties/server
    - [x] is kept private

- **In federated learning**

    - [ ] We control how the data is distributed across parties/workers
    - [x] Data in each party/worker is not indipendentent and identically distributed

- **In federated learning there is always a server to orchestrate the training**

    - [ ] True
    - [x] False

- **In the FedAVG algorithm the central model is updated**

    - [ ] Taking the minimum value of the parameters in the corrisponding layers across the models sent by the different workers
    - [x] Taking the mean value of the parameters in the corrisponding layers across the models sent by the different workers
    - [ ] Taking the median value of the parameters in the corrisponding layers across the models sent by the different workers
    - [ ] Taking the maximum value of the parameters in the corrisponding layers across the models sent by the different workers

- **GANs**

    - [x] learn to sample from the training set
    - [ ] learn to generate data from the training set
    - [ ] learn to interpolate the data in the training set

- **GANs are composed of two models called:**

    - [ ] Interpolator
    - [ ] Classificator
    - [x] Discriminator
    - [ ] Creator
    - [x] Generator
    - [ ] Inventor

- **The key layer in the generator is**

    - [ ] Canonical convolution
    - [ ] Inverted convolution
    - [ ] Interpolated convolution
    - [x] Transposed convolution
    - [ ] Dilated convolution

- **During the update of the Discriminator, the gradients flow through the Generator**
    
    - [ ] True
    - [x] False

- **During the update of the Generator, the gradients flow through the Discriminator**
    
    - [x] True
    - [ ] False

