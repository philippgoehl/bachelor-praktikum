# Torch

`Torch` originated in `2002` and was written in `Lua`, `C`, and `C++`.  
It provides a powerful framework for `tensor operations` and was designed specifically for `machine learning` and `scientific computing`.  
Torch offered fundamental routines for deep learning tasks but had limited accessibility for users outside the Lua ecosystem.

## PyTorch

`PyTorch`, developed by Facebook’s AI Research Lab (FAIR) and released in `2017`, is the modern successor to Torch.  
It is implemented in `Python`, `C++`, and `CUDA`, combining ease of use with high-performance GPU computation.  
PyTorch integrates seamlessly with the Python data science ecosystem, making it one of the most widely used frameworks for deep learning today.

Key advantages include:

- Dynamic computation graphs (“define-by-run”) for flexible model building
- Strong GPU acceleration
- Extensive ecosystem (e.g., `torchvision`, `torchaudio`, `torchtext`)
- Support for deployment and optimization through `TorchScript` and `PyTorch Lightning`

## PyTorch Datasets & Dataloader

### Datasets

PyTorch provides many `standard datasets` through the `torchvision.datasets` module — for example, the well-known `CIFAR-10` and `CIFAR-100` datasets used for image classification tasks.

You can find an overview here: [PyTorch Vision Datasets](https://pytorch.org/vision/main/datasets.html)

Developers can also create `custom datasets` by subclassing `torch.utils.data.Dataset`.

### Dataloader

During training, data is typically processed in `mini-batches` — smaller groups of samples rather than the entire dataset at once.  
Mini-batching improves computational efficiency and stabilizes gradient updates.

The `Dataloader` class in PyTorch provides a high-level interface for:

- Splitting data into mini-batches
- Shuffling samples randomly in each epoch
- Loading data asynchronously in parallel using multiple workers

This abstraction allows efficient and scalable data feeding for model training.
