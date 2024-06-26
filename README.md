# MedIMeta for PyTorch

## Medical Imaging Meta Dataset

We release the MedIMeta Dataset, a novel meta dataset comprised of 17 publicly available
datasets containing a total of 28 tasks. We additionally prepared a private set of tasks
derived from different datasets which will be used for validation and final testing of
the submissions. All datasets included in the MedIMeta dataset have been previously
published under a creative commons licence. The dataset bears similarity to, and has
partial overlap with, the Medical MNIST dataset. However, we go beyond Medical MNIST in
the amount and diversity of tasks included in our dataset. Moreover, all images in
MedIMeta are standardized to an image size of 224x224 pixels which allows a more
clinically meaningful analysis of the images. The MedIMeta dataset and this library
provide a resource for quickly benchmarking algorithms on a wide range of medical tasks.

You can see details about the MedIMeta dataset as well as download the dataset from
[https://www.l2l-challenge.org/data.html](https://www.l2l-challenge.org/data.html).

## PyTorch Library

This library allows easy access to all tasks in the MedIMeta dataset as PyTorch datasets.
It provides a unified interface to the data and allows for easy usage in PyTorch.
The MedIMeta library integrates with
[TorchCross](https://www.github.com/StefanoWoerner/torchcross), a PyTorch library for
cross-domain learning, few-shot learning and meta-learning. It is therefore easy to
use the MedIMeta dataset in conjunction with TorchCross to perform cross-domain learning,
few-shot learning or meta-learning experiments.

**This library is still in alpha. The API is potentially subject to change. Any feedback
is welcome.**

## Installation

The toolbox can be installed via pip:

```bash
pip install medimeta
```

## Basic Usage

The MedIMeta dataset can be accessed via the `medimeta.MedIMeta` class, which extends the 
`torch.utils.data.Dataset` class. See the basic example below:

```python
from medimeta import MedIMeta

# Create the dataset for the Disease task of the OCT dataset, assuming
# the data is stored in the "data/MedIMeta" directory
dataset = MedIMeta("data/MedIMeta", "oct", "Disease")

# Get the first sample
sample = dataset[0]

print(sample[0].shape)
print(sample[1])
```

This will print the following:

```bash
torch.Size([1, 224, 224])
0
```


## Advanced Usage

MedIMeta builds on top of [TorchCross](https://www.github.com/StefanoWoerner/torchcross),
a library for cross-domain learning, few-shot learning and meta-learning in PyTorch.
MedIMeta can be used in conjunction with TorchCross to easily create cross-domain learning
or few-shot learning experiments. To this end, MedIMeta provides two convenience classes
for generating batches from multiple MedIMeta tasks and for generating few-shot insttances
of multiple MedIMeta tasks.

### Examples

See the [examples](examples) directory for examples on how to use MedIMeta in conjunction
with [TorchCross](https://www.github.com/StefanoWoerner/torchcross).
- [`imagenet_pretrained.py`](examples/imagenet_pretrained.py) shows how you can test
  pre-trained models on a few-shot instance of a MedIMeta task.
- [`cross_domain_pretraining.py`](examples/cross_domain_pretraining.py) shows how you
  can perform cross-domain pre-training on different MedIMeta tasks and then test the
  pre-trained model on a few-shot instance of a MedIMeta task.
- [`cross_domain_maml.py`](examples/cross_domain_maml.py) shows how you can perform
  cross-domain meta-learning with [MAML](https://arxiv.org/abs/1703.03400) on different
  MedIMeta tasks and then test the meta-learned model on multiple few-shot instances of a
  MedIMeta task.
- [`fully_supervised.py`](examples/fully_supervised.py) shows how you can perform
  fully-supervised learning on MedIMeta tasks by using the TorchCross `SimpleClassifier`.
