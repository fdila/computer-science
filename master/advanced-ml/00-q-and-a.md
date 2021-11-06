% Advanced Machine Learning Questions, 2021/2022
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
    - [ ] Factor of variations is directly observable
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