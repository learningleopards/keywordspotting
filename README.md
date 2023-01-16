# Keyword Spotting using Edge Impulse

#### Table of contents

<br>

[1.0 Introduction](#10-introduction)

[2.0 Objective](#20-objective)

[3.0 Previous Works](#30-previous-works)

[4.0 Use Cases](#40-use-cases)

[5.0 System Architecture](#50-system-architecture)

[6.0 Algorithm](#60-algorithm)

[7.0 Discussion](#70-discussion)

[8.0 References](#80-references)


## 1.0 Introduction

We explore a keyword-based spoken language understanding system, in which the intent of the user can directly be derived from the detection of a sequence of keywords in the query. We focus on the keyword spotting method and edge impulse which is the leading development platform for machine learning on edge devices and free for developers. Edge impulse is used to perform audio data classification.

## 2.0 Objective

To perform audio classification model training using edge impulse.
Integrating the trained classifier model into the Nucleo-F446RE board.
Perform an experiment to integrate the microphone with the classifier to perform real-time sound classification.

## 3.0 Previous Works

Keyword spotting(KWS) is a critical component for enabling speech based user interactions on smart devices. It requires real-time response and high accuracy for good user experience. Recently, neural networks have become an attractive choice for KWS architecture because of their superior accuracy compared to traditional speech processing algorithms. In previous work on keyword spotting on microcontrollers, the neural network architecture evaluation and exploration for running KWS on resource-constrained microcontrollers is performed. Trained various neural network architectures for keyword spotting published in literature to compare the accuracy and memory or compute requirements. The work has shown that it is possible to optimize the neural network architecture to fit within the memory and compute constraints of microcontrollers without sacrificing accuracy.

## 4.0 Use Cases
![image](https://user-images.githubusercontent.com/92903308/209988352-1c8fbe66-d4de-479a-956f-b9c9cf46e7d0.png)

![image](https://user-images.githubusercontent.com/92903308/209988403-8de28f1f-e491-4ee8-aac0-bb9800cd5e3b.png)


## 5.0 System Architecture

The figure below shows the overall flow of the data. At first, the sound is collected with an inmp441 esp32 microphone. Then, the sound data is populated into the NUCLEO-F446RE board through the SAI ports enabled. SAI is a protocol that allows the stm32 microcontroller to communicate with audio devices and the other ADC/DAC. In this project, SAI serves as the agent to convert sound data to digital bits to be analyzed by the classifier in the microcontroller.

![image](https://user-images.githubusercontent.com/92903308/209988520-411d8803-7295-4f93-96db-7403fe5f0e97.png)

## 6.0 Algorithm

Edge impulse is used to perform audio data classification. It is a very user-friendly application that allows the users to implement the Neural Network algorithm. An artificial intelligence technique called a neural network instructs computers to analyze data in a manner modeled after the human brain. Deep learning is a sort of machine learning that employs interconnected neurons or nodes in a layered framework to mimic the human brain. It develops an adaptive system that computers utilize to continuously learn from their errors and improve. Artificial neural networks make an effort to more accurately tackle complex issues, such as summarizing documents or identifying faces. STM32Cube.Al is a free programme that imports pre-trained machine learning or neural network models and converts them into STM32-optimized C code. These days, embedded hardware devices must handle more difficult Al tasks. ST provides a complete environment, which includes a potent neutral network conversion tool called STM32Cube, to aid developers in building creative applications. STM32Cube.Al is a tool for users who have prior experience in creating and training deep learning NN models in frameworks such as Tensorflow Lite, Keras, qKeras or Pytorch. STM32Cube.Al allows to convert pre-trained neural networks into optimized code for STM32 microcontrollers.

## 7.0 References
1. Projects/Supervision (no date) Mun'im Zabidi. Available at: http://raden.fke.utm.my/projects (Accessed: January 7, 2023).
2. Smales, M. (2021) Sound classification using Deep Learning, Medium. Medium. Available at: https://mikesmales.medium.com/sound-classification-using-deep-learning-8bc2aa1990b7 (Accessed: January 7, 2023).
3. Zhang, Y. et al. (2018) Hello edge: Keyword spotting on microcontrollers, arXiv.org. Available at: https://arxiv.org/abs/1711.07128 (Accessed: January 7, 2023).

