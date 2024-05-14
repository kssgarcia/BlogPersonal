---
title: "Neural networks"
date: 2023-07-13T11:48:52-05:00
draft: false
---

## Introduction

In recent years, advances in Deep Learning, and in particular in neural networks, have revolutionized the field of artificial intelligence. Thanks to their ability to learn autonomously from large amounts of data, neural networks have succeeded in pushing the limits of performance in a variety of tasks.

One of the areas in which neural networks have had a significant impact is image recognition and computer vision. By using architectures such as convolutional neural networks (CNN), surprising results have been achieved in object classification, object detection, and semantic segmentation.

Structural optimization is a fundamental challenge in the field of engineering, where the goal is to find efficient and economical designs for structures that meet specific load requirements and constraints. In this search for optimal solutions, neural networks have emerged as a powerful tool in structural optimization. With their ability to machine learn and model complex relationships, neural networks offer an innovative way to improve the efficiency and performance of structures. In this introduction, we will explore how neural networks are applied in structural optimization, highlighting their potential to generate optimal designs and revolutionize structural engineering.

In this article, the results of the background review on Deep Learning and the different algorithms currently presented will be presented, revealing the most convenient architectures to solve these problems and the different ways of implementing these networks to traditional optimization algorithms.

## Types of neural networks

Deep learning, known as Deep Learning in English, is a branch of artificial intelligence that is based on the construction and training of artificial neural networks so that they can learn and perform tasks autonomously. Unlike traditional machine learning algorithms, which require careful feature selection and expert knowledge to extract patterns from data, deep learning focuses on enabling neural networks to learn automatically from large volumes of data without guidance. or explicit preprocessing.

Deep neural networks are made up of multiple layers of interconnected processing units called neurons. Each layer extracts progressively more abstract and complex features as it progresses through the network, allowing for a hierarchical representation of the data. This deep architecture allows the model to learn high-level features and build a more sophisticated understanding of the input data.

Training a deep neural network involves presenting it with labeled examples and adjusting the weights and connections between neurons so that the model can make accurate predictions. This process is carried out through the use of error optimization and back propagation algorithms, which allow the calculation of the contribution of each neuron and adjust the parameters in such a way that the error between the model predictions and the real labels is minimized.

Within neural networks, different architectures are presented that aim to abstract different functions that are better suited to the task to be performed, such as image classification, natural language processing, among others. In this article three types of architectures will be presented which are commonly used in structural optimization methods:


### Multilayer neural network

A multilayer neural network is an architecture of artificial neural networks that consists of multiple layers of interconnected processing units called neurons, this architecture is the simplest, so its learning capacity is more limited than other neural networks, however it is presented in This article because it can contain the general idea that covers all the architectures present in neural networks. This layered structure allows for more complex data learning and representation, making it a powerful tool in the field of machine learning and information processing.

In a multilayer neural network, three main types of layers are distinguished: input layer, hidden layers, and output layer. The input layer receives the input data and passes it on to the next layer, which is usually a hidden layer. Hidden layers, as the name suggests, sit between the input layer and the output layer and are responsible for learning and extracting more abstract and complex features as you go deeper into the network. Finally, the output layer generates the predictions or desired results based on the specific task at hand.

Each neuron in a multilayer neural network is connected to neurons in neighboring layers by weighted connections. These connections represent the force of influence that one neuron has on another. Each neuron in a layer receives inputs from the neurons in the previous layer, multiplies them by the corresponding weights and the bias of said neuron. The bias allows a neural network to learn and represent more complex and non-linear relationships between the input and output variables, this parameter is weightedly added to the linear combination of the inputs before applying the neuron activation function, after doing the weighted sum is passed through a nonlinear activation function. The activation function introduces nonlinearity into the model and allows the neural network to capture complex, nonlinear relationships between variables.

Training a multilayer neural network involves adjusting the connection weights and bias for each neuron so that the model can make accurate predictions. This is achieved by using learning algorithms, such as error backpropagation, which calculates the difference between the model predictions and the actual labels and adjusts the weights based on this error. The training process is repeated iteratively until the model reaches a desired level of accuracy. Backpropagation is done by implementing optimization algorithms such as gradient descent. In a simple way, in a multilayer neural network, what is happening in each training cycle is evaluating the network (forward), initially with random weights and bias, and then backpropagation is applied to calculate the sensitivity of the network parameters with the error function to be able to update these parameters in order to minimize the error. The error or cost function varies depending on the problem being performed.

#IMAGESSSSS

### Convolutional Network

A convolutional network, also known as a convolutional neural network (CNN), is a type of neural network architecture specifically designed to process data with a grid structure, such as images. It is characterized by the inclusion of convolutional layers, which apply convolution filters to extract visual features, and pooling layers, which reduce the dimensionality of the data.

Convolutional networks are highly effective in computer vision related tasks such as object recognition, object detection, image segmentation, and image classification. This is because convolutional layers can learn local and hierarchical features from images, such as edges, textures, and shapes, and pooling layers allow invariance to small deformations and displacements.

In structural optimization by means of neural networks, a variation of this neural network, encoder and decoder network based on CNN, is commonly used. The difference between this architecture and conventional CNN is that it consists of an encoder and a decoder, both based on in convolutional layers.

The encoder, also known as a feature extraction network, is responsible for capturing and compressing the relevant information from an image into a lower-dimensional representation. It uses convolutional layers to extract high-level features from the image input, such as edges, textures, and shapes. These convolutional layers are often followed by pooling or subsampling layers to reduce spatial resolution and keep only the most important features. The decoder, on the other hand, is in charge of reconstructing an image from the low-dimensional representation generated by the encoder. It uses transposed convolutional layers, also known as deconvolution layers, to gradually increase the spatial resolution and produce an output image that closely resembles the original image. The decoder can also include additional convolution layers to further refine the reconstruction and improve fine detail.

The connection between the encoder and the decoder is made through a hopping connection, which allows information from the high-level layers of the encoder to be transmitted directly to the decoder. This connection helps to merge the features extracted by the encoder with the spatial information from the decoder, which allows a better reconstruction of the final image.

### Adversarial generative neural network

A Generative Adversarial Neural Network (GAN) is a type of neural network architecture composed of two main components: a generator and a discriminator. GAN is used to generate synthetic data, such as images, music, or text, that resembles real data.

The generator is responsible for creating synthetic samples from a random input space, such as noise vectors. As the generator learns during training, it attempts to generate data that is indistinguishable from the actual data.

The discriminator, on the other hand, acts as a classifier that tries to distinguish between the samples generated by the generator and the actual samples. Its objective is to learn to discriminate between the generated data and the real data.

During GAN training, the generator and discriminator train adversarially, competing against each other. The generator tries to fool the discriminator by generating more and more realistic samples, while the discriminator is trained to be more accurate in detecting the generated samples. This competition creates a feedback loop where both components are continuously improved.

The ultimate goal of a GAN is for the generator to be able to give high-quality synthetic samples that are indistinguishable from the real data, while the discriminator becomes less and less capable of differentiating between the generated samples and the real samples.

GANs have proven effective in generating realistic images, natural language processing, and other data generation tasks.


# References

[1] 3Blue1Brown. (2017, October 5). But what is a neural network? —Chapter 1, Deep Learning.
Youtube. https://www.youtube.com/watch?v=aircAruvnKk
[2] arlethv. (2022, September 19). Recursive Neural Network in Deep Learning. https://forum.huawei.
com/enterprise/en/recursive-neural-network-in-deep-learning/thread/1003551-100757
[3] Chandrasekhar, A., Sridhara, S., & Suresh, K. (2022). GM-TOuNN: Graded Multiscale Topology
Optimization using Neural Networks.
[4] Sosnovik, I., & Oseledets, I.V. (2017). Neural networks for topology optimization. CoRR, abs/1709.09578.
http://arxiv.org/abs/1709.09578
[5] Xiang, C., Chen, A., & Wang, D. (2022). Real-time stress-based topology optimization via deep lear-
none. Thin-Walled Structures, 181, 110055. https://doi.org/https://doi.org/10.1016/j.tws.
2022.110055
[6] Yu, Y., Hur, T., Jung, J., & Jang, I.G. (2018). Deep learning for determining a near-optimal topological
design without any iteration. Structural and Multidisciplinary Optimization, 59 (3), 787-799.
https://doi.org/10.1007/s00158-018-2101-5
[7] Zhang, Y., Peng, B., Zhou, X., Xiang, C., & Wang, D. (2020). A deep Convolutional Neural Network
for topology optimization with strong generalization ability.
9