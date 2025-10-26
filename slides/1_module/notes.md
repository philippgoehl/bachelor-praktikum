# What is Machine Learning?

**Machine Learning (ML)** is a method of teaching computers to recognize patterns in data and make predictions or decisions without being explicitly programmed.

In essence, it is a form of **data fitting**, where we aim to find the optimal

- **model parameters** w ∈ W
- for a given **input** x ∈ X
- and **output** y ∈ Y
- within a **model** h(·; w )
- such that: h(x; w) = y

## Types of Machine Learning

Machine Learning can be broadly categorized into three types:

- **Supervised Learning** (e.g., classification, regression)
- **Unsupervised Learning** (e.g., clustering, dimensionality reduction)
- **Reinforcement Learning** (e.g., robot navigation, game strategies)

In **supervised learning**, the data is labeled, and the model learns from examples with known outcomes. The model receives feedback indicating whether its predictions are correct, allowing it to adjust and improve over time.

In **unsupervised learning**, by contrast, the data is unlabeled. The model must discover hidden patterns or structures in the data on its own, such as grouping similar items or identifying latent features.

In **reinforcement learning**, an agent interacts with an environment and learns optimal actions through trial and error, guided by rewards and penalties.

## Artificial Neural Networks (ANNs)

**Artificial Neural Networks (ANNs)** are computational models inspired by the human brain’s structure. They are particularly effective for complex tasks such as **image classification**, **speech recognition**, and **natural language processing**.

**Example**:
Input x ∈ X: a lot of pictures.
ANN h(·; w ): a lot of parameters
Output y ∈ Y: cat / dog

### Artificial Neuron

An **artificial neuron** processes weighted inputs from preceding neurons and outputs a signal to the next layer when activated.  
It can be represented mathematically as a **weighted sum** followed by an **activation function**.

![An artificial neuron as function of a weighted sum](./images/artificial-neuron.png)

### Activation Functions

**Activation functions** determine when a neuron should "fire" and introduce non-linearity into the network, enabling it to learn complex patterns.

![Activation functions](./images/activation-functions.png)

### Feed-Forward Neural Network

A **Feed-Forward Neural Network (FNN)** is a type of Artificial Neural Network where the information flows in one direction — from the input layer, through one or more hidden layers, to the output layer.  
Each neuron passes its output to the next layer without feedback loops.

![Feed-Forward Neural Network](./images/feed-forward-neural-network.png)

## Convolutional Neural Networks (CNNs)

For more complex data structures, such as 2D arrays (e.g., images), **Convolutional Neural Networks (CNNs)** are used.  
CNNs apply convolutional filters that capture spatial hierarchies and local dependencies in the data.  
This approach bridges the gap between small networks that lack expressive power and large networks that risk **overfitting**.

![CNNs](./images/cnns.png)

## Overfitting

Overfitting occurs when a machine learning model learns the training data too well, including its noise and outliers, resulting in excellent performance on training data but poor generalization to new, unseen data. In other words, the model becomes too specialized to the training set and fails to capture the underlying patterns that apply more broadly.

## The Loss Function

The **loss function** measures how far the model’s predictions are from the actual target values.  
This quantified error is used to adjust the model’s parameters and improve its accuracy during training.

### Mean Square Error (MSE)

![MSE](./images/mse.png)

The **Mean Square Error (MSE)** measures the average squared difference between the predicted values and the actual (true) values.  
It quantifies how close the model’s predictions are to the real outcomes — smaller values indicate better performance.  
Because the errors are squared, larger mistakes are penalized more heavily, making MSE particularly sensitive to outliers.

### Cross-Entropy-Loss (binary Classification)

![CE](./images/ce.png)

Here, C denotes the set of classes, β is a binary indicator (e.g., ±1), and p\_{o,c} represents the predicted probability that an object o belongs to class c.

The **cross-entropy loss** measures the difference between the predicted probability distribution and the true class labels.  
It penalizes confident but incorrect predictions more strongly, encouraging the model to output probabilities that reflect true likelihoods.

## Optimizer

An **optimizer** is an algorithm that adjusts the model’s parameters to minimize the loss function and improve performance over time.

### Gradient Descent (GD)

One of the most common optimization methods is **Gradient Descent (GD)**.  
This iterative approach updates model parameters by moving them in the direction that most reduces the loss — the **negative gradient**.

Each iteration determines:

- a **step direction** — the gradient of the loss function, and
- a **step size** — the _learning rate_, controlling how far the update moves.

Through repeated updates, the optimizer converges toward parameters that minimize the loss and improve the model’s predictions.

![Gradient Descent](./images/gradient-descent.png)

## Training the Network

## Backpropagation

To train a neural network, we need to communicate the **error or deviation** of the output back through the network to adjust its parameters.  
This process is called **backpropagation**.

During backpropagation, the gradient of the loss function with respect to each weight and bias is computed by applying the **chain rule** of calculus.  
This allows the network to determine how each parameter contributed to the overall error.

![Backpropagation Formula](./images/backpropagation-formula.png)

The weights and biases are then updated to reduce this error, gradually improving the model’s predictions.

**Illustration:**  
The deviation between the model’s prediction and the true value is measured and propagated backward through the network.  
Due to the chain-linked dependencies of neurons, this propagation proceeds iteratively from the output layer back to the input layer — a process known as **backpropagation**.

![Backpropagation](./images/backpropagation.png)
