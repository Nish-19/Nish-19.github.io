---
layout: post
title: Introduction to Transfer Learning
---
![TRANSFER_LEARNING-512](https://user-images.githubusercontent.com/41947720/79555971-0852b100-80be-11ea-9b40-d2f6f1df7543.png)

In recent times, we have become extremely capable of training deep neural networks to learn accurate mappings on typical supervised learning tasks like the classification of images, text, etc.

Do these "accurate" neural networks have the ability to generalize well on all kinds of datasets?

Sadly, the answer is NO. This is because it has to do with the type of the dataset under consideration.

In contrast to a well-constructed one, a real-world dataset generally comprises of a lot of noise and many novel scenarios that the neural network would have never seen before, hence leading to poor results.

So, what can be done here?

This is where transfer learning comes. In layman terms, the ability to transfer knowledge to new scenarios is called Transfer Learning.

Typically, if we have a state of the art (or any well-performing) model say M, on a particular dataset A, and we want to extend it to another domain B, then transfer learning comes to help. Transfer learning involves using the highly accurate model M, by keeping the initial layers, and only tweaking (or making changes to the final layer) so that it transforms and performs well on domain B as well.

<Picture>

##Advantages

* Useful when there is a dearth of training data for the target task.
* The overall model becomes faster to train.

However, one limitation is that this method can be used only when the features learned from the source task are general, i.e., the features must be in suitable for the target task as well.

Having said this, let's see how we can use transfer learning practically.

###Pre-trained Model Approach
1) Selecting source model: Here we select a pre-trained model from among the available ones, which we think is the most suited for our task. There are plenty of such models freely available to choose from.
2) Reuse Model: This model is then used for the target task. Here we may have to take care of things like how to input the data, how many layers should we use from the model etc.
3) Tune Model: After making it suitable for the task, we may go further by adding additional layers upon the pre-trained model and make it well suited to our target task.
