---
title: "My first neural network"
date: 2023-08-03T11:48:52-05:00
draft: false
---

In the last few decades, neural networks have emerged as a powerful tool in the field of machine learning and artificial intelligence. These artificial networks have demonstrated their effectiveness in a wide range of applications, from speech recognition and computer vision to automatic translation and user behavior prediction.

A neural network is a computational model composed of interconnected units called neurons, which work together to process and learn complex patterns from data. These networks are organized into layers, where each layer consists of multiple neurons that process information and transmit signals through weighted connections.

The flexibility and adaptability of neural networks have made them a promising tool for various applications, as they can learn automatically from examples and generate accurate predictions. In the field of topology optimization, which aims to find the optimal configuration of a given system or structure, neural networks have also proven to be highly valuable. Topology optimization involves determining the optimal distribution of material within a given region, maximizing structural efficiency, or minimizing some cost metric.

The integration of neural networks into topology optimization has allowed overcoming the limitations of traditional approaches, which often rely on heuristic methods or specific algorithms to solve optimization problems. By using neural networks, it is possible to obtain faster and more efficient solutions, as these networks can learn to recognize patterns and key features in input data.

In particular, neural networks can assist in the automatic generation of optimal designs in topology optimization. By training a neural network with input data representing the problem's boundary conditions and constraints, along with corresponding output representing the optimal design, the network can learn to efficiently and accurately generate optimized structural designs.

This report describes the process of building a convolutional neural network that takes boundary conditions and problem constraints as input data and produces the density distribution of the optimal design. For this purpose, data was generated using the Solid Isotropic Material Penalization (SIMP) method. Section 2 presents the step-by-step construction of the neural network: 2.1 explains the data generation process, 2.2 outlines the neural network architecture, subsection 2.3 covers the training phase, and finally, Section 3 presents the results.

## 2. Neural Network

To solve the structural optimization problem, a convolutional neural network was chosen due to the data structure's compatibility with this problem. This neural network was based on the approach proposed by Yu et al. (2018), where a convolutional neural network and a generative adversarial network were also employed.

To construct this network, sample data was first generated using the traditional SIMP method. This method employs the solid elements scheme, where each element has a relative density. This density distribution is taken as the output for the neural network. The neural network has two input channels of size 61x61, representing the boundary conditions, constraints, and volume fraction. The output is a single channel of size 60x60.

## 2.1. Sample Generation

Figure 1 illustrates the data generation process. A grid of 60x60 elements was used for this purpose. To format the input and output data for processing by the neural network, two 2D matrices were organized: one containing the boundary conditions (3 channels) and the other containing the constraints and volume fraction (2 channels). Data generation was performed using a custom [code](https://github.com/kssgarcia/DeepLearningOpt/blob/main/simp/SIMP_multi.py), utilizing the [SolidsPy](https://github.com/AppliedMechanics-EAFIT/SolidsPy) package.

![Picture 1](/generacion.png)
|:--:|
| **Figure 1. Data generation scheme.** |

![Picture 1](/canal1.jpg)
|:--:|
| **Figure 2. Matrix for constraint and volume fraction channel.** |

![Picture 1](/canal2.jpg)
|:--:|
| **Figure 3. Matrix for boundary conditions channel.** |


## 2.2. Architecture

The architecture of the neural network is depicted in Figure 4. This network consists of 11 layers, which can be divided into down-sampling layers and up-sampling layers.

![Picture 1](/arquitec.png)
|:--:|
| **Figure 4. Neural network architecture.** |



## Training

For training, 3660 samples were taken, corresponding to variations in load within the green region shown in Figure 5. This training took approximately 4.83 hours. With this data, training was conducted over 6 epochs using the Adam optimizer, requiring 11.31 hours. [Code](https://github.com/kssgarcia/DeepLearningOpt/blob/main/simp/SIMP_multi.py)

![Picture 1](/cargas.jpg)
|:--:|
| **Figure 5. Data generation scheme.** |


![Picture 1](/entrenamiento.png)
|:--:|
| **Figure 6. Data training scheme.** |

## Results 

As depicted in Figure 7, some of the results show a significant resemblance to the expected outcome. Discrepancies arise in the gray zones, where the expected beam's result appears smoother.

![Picture 1](/FNNresultados.png)
|:--:|
| **Figure 7. Training results.** |


## Conclusions

Topology optimization involves finding the optimal material distribution in a structure to meet performance criteria, such as minimizing weight or maximizing stiffness. Traditionally, this task has been challenging due to problem complexity and the need for multiple iterations. However, with the emergence of neural networks, a new approach to topology optimization has opened up. There are various schemes for implementing these methods in structural optimization; the one presented in this article is particularly interesting due to its non-iterative nature, aiming to leverage the full potential of machine learning tools, albeit demanding more effort. Building these models requires a significant amount and variety of data samples. The greater the sample size, the more patterns can be recognized.

## References

Yu, Y., Hur, T., Jung, J., & Jang, I. G. (2018). Deep learning for determining a near-optimal topological
design without any iteration. Structural and Multidisciplinary Optimization, 59 (3), 787-799.
https://doi.org/10.1007/s00158-018-2101-5
