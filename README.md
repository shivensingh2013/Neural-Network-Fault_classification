# Multi-objective optimization based recursive feature elimination for process monitoring

__Build Date__ : 21 May 2019 \
__Build Author__ : Shivendra Singh

### Description : 
This project proposes an optimization based features selection for process monitoring, that simultaneously trades-off between the optimal features selection and the resulting model complexity, 
by means of solving a multi-objective optimization problem.In particular, this code focuses on combining neural network architecture with recursive feature elimination and genetic algorithm to obtain higher fault identification accuracy while reducing 
the number of variables to be measured continuously in the process plant.

### Methodology :
The code structure can be broken down into the following components : 
1. __Dimension reduction by using Recursive feature elimination__ \
Recursive Feature Elimination (RFE) uses a ranking criterion to select important features, recursively. At each iteration, based on the feature ranks, less relevant features are eliminated. The final ranking would be determined based on the inverse order in which features are eliminated and only first n features are used further. Support Vector Machine (SVM) and Random Forest (RF) are the two main estimators used for ranking the features \cite{granitto2006recursive}. In this study, we have chosen RF based estimator along with RFE for dimension reduction.
2. __Neural net (NN) based classification for process monitoring__ \
We consider a feedforward network for modeling the process data. . Once, the underlying model is built on the training data, it can be used for classifying the test data-sets to normal and faulty.We employ categorical cross entropy cost function to penalize the data and to obtain the model parameters.\
Cross-entropy loss measures the performance of a classification model whose output probability ranges between 0 and 1. Cross-entropy penalization increases when the predicted probability diverges from the true label. The optimization problem is solved using stochastic gradient descent approach. We have also used various improved version of stochastic gradient descent including, __AdaGrad__ (adaptive stochastic gradient algorithm), __RMSProp__ (the learning rate is adapted as a __Root Mean Square Propagation__ ), and __Adam__ (adaptive moment estimation both the gradients and the second moments of the gradients are employed) for training the NN . Over-fitting and performance tuning are two major factors to be considered while designing an NN. The __early stopping technique__ has been used for detecting over-fitting in the network.\
For paramtere tuning ,the tuning of the number of neurons present in the hidden layer and the number of hidden layers, training size ratio and the number of features selected for training has been done using genetic algorithm whereas other parameters such as activation function, training batch size and learning rate have been tuned manually.
3. __Multi-objective optimization based feature selection for improved process monitoring:  a genetic algorithm based solution approach__  \
In this work, a population of initial solutions generated randomly are encoded in a genetic form and operated with genetic operations such as crossover and mutation to improve these iteratively over a number of generations finally leading to a population of optimal solutions. Here, Real-coded form of NSGA-II algorithm for optimization has been used due to its simplicity of design and low computational complexity.
4. __Online monitoring__ \
Once the model is trained, it can be deployed for online monitoring. While doing so, firstly the incoming data sample is normalized and  important features are selected by RFE. This sample is finally passed into the model for prediction and a fault is identified if the same prediction persists after successive samples. 
