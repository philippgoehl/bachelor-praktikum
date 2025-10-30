# Task 3: Federated Learning (10 Points)

Expand your code by now distributing the data set identically to 10 clients (randomly!) and only exchanging parameters with a (parameter) server.

This sends an update of the weights to all clients after applying a suitable strategy.

Use Federated Averaging (FedAvg) as a strategy and update after a local gradient step (Round).

Visualize your results.

## Tips:

- One (local) gradient step is executed for each (local) minibatch.
- The global minibatch is a combination of local minibatches and the number of clients.
