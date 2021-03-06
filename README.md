# Adversarial-Attacks-Pytorch

[![License](https://img.shields.io/github/license/Harry24k/adversarial-attacks-pytorch)](https://img.shields.io/github/license/Harry24k/adversarial-attacks-pytorch)
[![Pypi](https://img.shields.io/pypi/v/torchattacks.svg)](https://img.shields.io/pypi/v/torchattacks)
[![Documentation Status](https://readthedocs.org/projects/adversarial-attacks-pytorch/badge/?version=latest)](https://adversarial-attacks-pytorch.readthedocs.io/en/latest/)

This is a lightweight repository of adversarial attacks for Pytorch.

[Torchattacks](https://arxiv.org/abs/2010.01950) is a PyTorch library that contains adversarial attacks to generate adversarial examples and to verify the robustness of deep learning models.



## Table of Contents
1. [Usage](#Usage)
2. [Attacks and Papers](#Attacks-and-Papers)
3. [Documentation](#Documentation)
4. [Contribution](#Contribution)
5. [Recommended Sites and Packages](#Recommended-Sites-and-Packages)



## Usage

### :clipboard: Dependencies

- torch 1.2.0
- python 3.6



### :hammer: Installation

- `pip install torchattacks` or
- `git clone https://github.com/Harry24k/adversairal-attacks-pytorch`

```python
import torchattacks
atk = torchattacks.PGD(model, eps=8/255, alpha=2/255, steps=4)
adversarial_images = atk(images, labels)
```



###  :warning: Precautions

* **All images should be scaled to [0, 1] with transform[to.Tensor()] before used in attacks.** To make it easy to use adversarial attacks, a reverse-normalization is not included in the attack process. To apply an input normalization, please add a normalization layer to the model. Please refer to [the demo](https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/demos/White%20Box%20Attack%20(Imagenet).ipynb).

* **All models should return ONLY ONE vector of `(N, C)` where `C = number of classes`.** Considering most models in _torchvision.models_ return one vector of `(N,C)`, where `N` is the number of inputs and `C` is thenumber of classes, _torchattacks_ also only supports limited forms of output.  Please check the shape of the model’s output carefully.

* **`torch.backends.cudnn.deterministic = True` to get same adversarial examples with fixed random seed**. Some operations are non-deterministic with float tensors on GPU [[discuss]](https://discuss.pytorch.org/t/inconsistent-gradient-values-for-the-same-input/26179). If you want to get same results with same inputs, please run `torch.backends.cudnn.deterministic = True`[[ref]](https://stackoverflow.com/questions/56354461/reproducibility-and-performance-in-pytorch).




## Attacks and Papers

Implemented adversarial attacks in the papers.

The distance measure in parentheses.

* **Explaining and harnessing adversarial examples (Dec 2014)**: [Paper](https://arxiv.org/abs/1412.6572)
  - FGSM (Linf)
  
* **DeepFool: a simple and accurate method to fool deep neural networks (Nov 2015)**: [Paper](https://arxiv.org/abs/1511.04599)
  - DeepFool (L2)
  
* **Adversarial Examples in the Physical World (Jul 2016)**: [Paper](https://arxiv.org/abs/1607.02533)
  - BIM or iterative-FSGM (Linf)
  
* **Towards Evaluating the Robustness of Neural Networks (Aug 2016)**: [Paper](https://arxiv.org/abs/1608.04644)
  - CW (L2)
  
* **Ensemble Adversarial Traning: Attacks and Defences (May 2017)**: [Paper](https://arxiv.org/abs/1705.07204)
  - RFGSM (Linf)
  
* **Towards Deep Learning Models Resistant to Adversarial Attacks (Jun 2017)**: [Paper](https://arxiv.org/abs/1706.06083)
  - PGD (Linf)
  
* **Boosting Adversarial Attacks with Momentum (Oct 2017)**: [Paper](https://arxiv.org/abs/1710.06081)
  * MIFGSM (Linf) - :heart_eyes: Contributor [zhuangzi926](https://github.com/zhuangzi926)
  
* **Theoretically Principled Trade-off between Robustness and Accuracy (Jan 2019)**: [Paper](https://arxiv.org/abs/1901.08573)
  - TPGD (Linf)
  
* **Comment on "Adv-BNN: Improved Adversarial Defense through Robust Bayesian Neural Network" (Jul 2019)**: [Paper](https://arxiv.org/abs/1907.00895)
  - APGD or [EOT](https://arxiv.org/abs/1707.07397) + PGD (Linf)
  
* **Fast is better than free: Revisiting adversarial training (Jan 2020)**: [Paper](https://arxiv.org/abs/2001.03994)
  - FFGSM (Linf)
  



Clean | Adversarial
:---: | :---:
<img src="https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/pic/clean.png" width="300" height="300"> | <img src="https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/pic/pgd.png" width="300" height="300">



## Documentation

### :book: ReadTheDocs

Here is a [documentation](https://adversarial-attacks-pytorch.readthedocs.io/en/latest/index.html) for this package.



### :bell: ​Citation

If you want to cite this package, please use the following BibTex:

```
@article{kim2020torchattacks,
  title={Torchattacks: A Pytorch Repository for Adversarial Attacks},
  author={Kim, Hoki},
  journal={arXiv preprint arXiv:2010.01950},
  year={2020}
}
```



### :rocket: Demos

- **White Box Attack with Imagenet** ([code](https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/demos/White%20Box%20Attack%20(Imagenet).ipynb), [nbviewer](https://nbviewer.jupyter.org/github/Harry24k/adversarial-attacks-pytorch/blob/master/demos/White%20Box%20Attack%20%28Imagenet%29.ipynb)):  Using _torchattacks_ to make adversarial examples with the [Imagenet dataset](http://www.image-net.org/) to fool [Inception v3](https://arxiv.org/abs/1512.00567).

- **Black Box Attack with CIFAR10** ([code](https://github.com/Harry24k/adversarial-attacks-pytorch/blob/master/demos/Black%20Box%20Attack%20(CIFAR10).ipynb), [nbviewer](https://nbviewer.jupyter.org/github/Harry24k/adversarial-attacks-pytorch/blob/master/demos/Black%20Box%20Attack%20%28CIFAR10%29.ipynb)):  This demo provides an example of black box attack with two different models. First, make adversarial datasets from a holdout model with CIFAR10 and save it as torch dataset. Second, use the adversarial datasets to attack a target model.

- **Adversairal Training with MNIST** ([code](https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/demos/Adversairal%20Training%20(MNIST).ipynb), [nbviewer](https://nbviewer.jupyter.org/github/Harry24k/adversarial-attacks-pytorch/blob/master/demos/Adversairal%20Training%20%28MNIST%29.ipynb)):  This code shows how to do adversarial training with this repository. The MNIST dataset and a custom model are used in this code. The adversarial training is performed with PGD, and then FGSM is applied to evaluate the model.



### :anchor: Update Records

Update records can be found in [here](https://github.com/Harry24k/adversairal-attacks-pytorch/blob/master/Update%20Records.md).



## Contribution

Contribution is always welcome! Use [pull requests](https://github.com/Harry24k/adversarial-attacks-pytorch/pulls) :blush:



##  Recommended Sites and Packages

* **Adversarial Attack Packages:**
  
    * [https://github.com/IBM/adversarial-robustness-toolbox](https://github.com/IBM/adversarial-robustness-toolbox): Adversarial attack and defense package made by IBM. **TensorFlow, Keras, Pyotrch available.**
    * [https://github.com/bethgelab/foolbox](https://github.com/bethgelab/foolbox): Adversarial attack package made by [Bethge Lab](http://bethgelab.org/). **TensorFlow, Pyotrch available.**
    * [https://github.com/tensorflow/cleverhans](https://github.com/tensorflow/cleverhans): Adversarial attack package made by Google Brain. **TensorFlow available.**
    * [https://github.com/BorealisAI/advertorch](https://github.com/BorealisAI/advertorch): Adversarial attack package made by [BorealisAI](https://www.borealisai.com/en/). **Pytorch available.**
    * [https://github.com/DSE-MSU/DeepRobust](https://github.com/DSE-MSU/DeepRobust): Adversarial attack (especially on GNN) package made by [BorealisAI](https://www.borealisai.com/en/). **Pytorch available.**
    * https://github.com/fra31/auto-attack: An attack that is believed to be the strongest in existence. **TensorFlow, Pyotrch available.**
    
    
    
* **Adversarial Defense Leaderboard:**
  
    * [https://github.com/MadryLab/mnist_challenge](https://github.com/MadryLab/mnist_challenge)
    * [https://github.com/MadryLab/cifar10_challenge](https://github.com/MadryLab/cifar10_challenge)
    * [https://www.robust-ml.org/](https://www.robust-ml.org/)
    * [https://robust.vision/benchmark/leaderboard/](https://robust.vision/benchmark/leaderboard/)
    * https://github.com/fra31/auto-attack
    
    
    
* **Adversarial Attack and Defense Papers:**
  
    * https://nicholas.carlini.com/writing/2019/all-adversarial-example-papers.html: A Complete List of All (arXiv) Adversarial Example Papers made by Nicholas Carlini.
    * https://github.com/chawins/Adversarial-Examples-Reading-List: Adversarial Examples Reading List made by Chawin Sitawarin.
