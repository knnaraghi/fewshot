# Fellowship.AI Few-Shot Learning Challenge

## Introduction

This is an implementation of Siamese Networks for One-Shot Learning as described [here](https://www.cs.cmu.edu/~rsalakhu/papers/oneshot1.pdf). 
 Some aspects have not been implemented from the paper and additional techniques have been implemented as well. 
 The objective is to build a classifier that is capable of discerning whether images represent the same character or not 
 while being exposed to as few examples as possible.

## Installation

Make sure to have the listed versions (or the latest) of Keras installed with Tensorflow backend and their associated dependencies. 
 Also make sure to have the base Python machine learning libraries such as NumPy, Scipy, iPython, etc installed as well. 
```
Keras 2.1.2
TensorFlow 1.2.1
```

## The Omniglot Dataset 

Omniglot can be downloaded from [here](https://github.com/brendenlake/omniglot). 
 Omniglot is a dataset of 1623 handwritten digits from 50 different alphabets. 
 The training set consists of 30 alphabets and the evaluation set consists of 20 alphabets. 
 Omniglot can be considered the transpose of MNIST in which the amount of classes far outnumbers 
 the amount of examples for each class. 
 
 Make sure to download images_background.zip and images_evaluation.zip from the Python folder.
 Unzip the files so that each of the background images and evaluation images datasets have the following folder structure:

```
 images_background ---> alphabets --> characters
 images_evaluation ---> alphabets --> characters
```
 
Once you have completed the above, make sure to confirm that the image paths are correct for your system
 by editing the below code in the notebook.

```
path = ''
train_path = os.path.join(path, 'images_background')
valid_path = os.path.join(path, 'images_evaluation')
```

## Implementation
The implementation of this requires batching the training set into samples of images containing half the same image and half a different image. 
 The evaluation is batched with 20 images of which one is the correct image. 
 This (20-Way) one-shot task can be made easier by adjusting the N-WAY value in the code. 

```
N_WAY = 20
```

to

```
N_WAY = 5
```

 Data augmentation and layer-wise learning rates are not used here like in the original paper. 
 In addition, a contrastive loss function was used which provided improvement in performance. Be careful changing 
 any parameters or hyperparameters especially for the network utilizing contrastive loss. The model utilizing 
 contrastive loss was somewhat difficult to implement as either the model did not train at all or gradient 
 updates resulted in gradient explosion. The implementation of the contrastive loss function itself differs 
 from the standard one found as a utility in the Keras repository. 
 If you would like to train for more batch iterations you can do so by changing the variable in 
 the code below:

 ```
TRAIN_BATCH = 12000
```

## Acknowledgements

Thanks to [Soren Bouma](https://sorenbouma.github.io/blog/oneshot/) for their blog post 
 and implementation of which several parts were used.

Same thanks to [Tiago Freitas](https://github.com/Goldesel23/Siamese-Networks-for-One-Shot-Learning) for
 his implementation as well. 

Additional thanks to [this informative blog post](https://hackernoon.com/one-shot-learning-with-siamese-networks-in-pytorch-8ddaab10340e)
 as well.
 
Final thanks to [Rik Nijessen](https://github.com/gewoonrik/duplicate_prs) for 
 their implementation of contrastive loss. 
 
## Related Work
[1] **Matching Networks for One Shot Learning**, Oriol Vinyals, Charles Blundell, Timothy Lillicrap, Koray Kavukcuoglu and Daan Wierstra, https://arxiv.org/abs/1606.04080 , 2016 <br/>

[2] **Learning to Compare: Relation Network for Few-Shot Learning**, Flood Sung, Yongxin Yang, Li Zhang, Tao Xiang, Philip H.S. Torr, Timothy H. Hospedales, https://arxiv.org/abs/1711.06025 , 2018 <br/>