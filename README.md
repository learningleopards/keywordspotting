# Keyword Spotting using Edge Impulse

Table of contents

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

The figure below shows the overall flow of the data. At first, the sound is collected with Microphone Sensor Module KY-037 High Sensitivity Module Sound Detection. Then, the sound data is populated into the NUCLEO-F446RE board through the SAI ports enabled. SAI is a protocol that allows the STM32 microcontroller to communicate with audio devices and the other ADC/DAC. In this project, SAI serves as the agent to convert sound data to digital bits to be analyzed by the classifier in the microcontroller.

![image](https://user-images.githubusercontent.com/92903308/209988520-411d8803-7295-4f93-96db-7403fe5f0e97.png)

## 6.0 Algorithm

Edge impulse is used to perform audio data classification. It is a very user-friendly application that allows the users to implement the Neural Network algorithm. An artificial intelligence technique called a neural network instructs computers to analyze data in a manner modeled after the human brain. Deep learning is a sort of machine learning that employs interconnected neurons or nodes in a layered framework to mimic the human brain. It develops an adaptive system that computers utilize to continuously learn from their errors and improve. Artificial neural networks make an effort to more accurately tackle complex issues, such as summarizing documents or identifying faces. STM32Cube.Al is a free programme that imports pre-trained machine learning or neural network models and converts them into STM32-optimized C code. These days, embedded hardware devices must handle more difficult Al tasks. ST provides a complete environment, which includes a potent neutral network conversion tool called STM32Cube, to aid developers in building creative applications. STM32Cube.Al is a tool for users who have prior experience in creating and training deep learning NN models in frameworks such as Tensorflow Lite, Keras, qKeras or Pytorch. STM32Cube.Al allows to convert pre-trained neural networks into optimized code for STM32 microcontrollers.

## 7.0 Methodology

Edge Impulse is used to perform audio data classification. It is a very user-friendly application that allows the users to implement Neural Network algorithms without much coding knowledge. However, the users would still need to know what processing block, learning block to choose according to their dataset.

Data Acquisition
In data acquisition, 61 audio files are uploaded to Edge Impulse for processing. The uploaded data are randomly picked from a downloaded Urban8kSound folder. The audio files included 8 classes of sound which are “Baby Sound”, “Car Ambulance”, “Car Horn”, “Dog Bark”, “Drilling”, “Engine Idling”, “Gun Shot” and “Sewing Machine”. After uploading the dataset, it can be split into training and testing categories. Then, the uploaded dataset must be labeled accordingly. Figure 1 shows the interface of uploading existing data. 

![WhatsApp Image 2023-02-12 at 3 27 39 PM](https://user-images.githubusercontent.com/92903308/218303725-777e4046-5a1d-4d7b-81b3-e616fabe5c25.jpeg)

**Figure 1: Upload existing data**

Figure 2 shows the separation of training data and test data with 6 labels. For audio dataset, the data collected value is shown as total time length. 
![WhatsApp Image 2023-02-12 at 3 27 39 PM (1)](https://user-images.githubusercontent.com/92903308/218304548-87185e5c-1f0c-4d8a-9cdf-5d58bcabae5e.jpeg)

**Figure 2: Data Acquisition**

Impulse Design
After that, the dataset is now ready to create impulse. Under the create impulse tab, the processing block and learning block are required to be defined. In the processing block, MFCC and Spectrogram are available for audio dataset. Figure 3 shows the available processing block in Edge Impulse. Spectrogram is using linear spaced frequency scale whereas MFCC is using quasi-logarithmic spaced frequency scale, which is more similar to how the human auditory system processes sounds [1]. MFCC is chosen due to its more distinguishable detail. Based on the research done, MFCC is more suitable to be applied on CNN models owing to its better result on validation and testing. Furthermore, there are three learning blocks available for different varieties of dataset. For example, Neural Network, Transfer Learning as well as K-mean Anomaly Detection. Figure 4 shows the available learning blocks in Edge Impulse. While Neural Network is chosen due to its great performance on recognizing audio. Last, the selected processing block and learning block need to be saved for the next stage process.
![WhatsApp Image 2023-02-12 at 3 27 39 PM (2)](https://user-images.githubusercontent.com/92903308/218304650-7d1d22e5-1727-4689-8574-ad1fc05861db.jpeg)

**Figure 3: Processing blocks**

![WhatsApp Image 2023-02-12 at 3 27 39 PM (3)](https://user-images.githubusercontent.com/92903308/218304722-1e51f44d-0c42-4874-b1bf-c704b34c6514.jpeg)

**Figure 4: Learning blocks**

![WhatsApp Image 2023-02-12 at 3 27 40 PM](https://user-images.githubusercontent.com/92903308/218304765-076528ee-4d05-4c3f-89d5-afb34d22a92c.jpeg)

**Figure 5: Create Impulse**

Mel Frequency Cepstral Coefficients are customizable by defining the available parameters. Figure 6 shows the default value for each of the parameters. After all the parameters are configured, save the parameters. 

![WhatsApp Image 2023-02-12 at 3 27 40 PM (1)](https://user-images.githubusercontent.com/92903308/218304911-f2d0efc8-4ad5-4ef9-8a04-b06ec583ce37.jpeg)

**Figure 6: Parameters of Mel Frequency Cepstral Coefficients
**

Figure 7 represents the signal form of one audio data. Other audio data could be surfed by selecting through the drop box. Figure 8 represents the Cepstral Coefficients of the highlighted region of the signal. 

![WhatsApp Image 2023-02-12 at 3 27 40 PM (2)](https://user-images.githubusercontent.com/92903308/218305070-ae2b4d35-417c-468b-ae91-5aeed3ea6f76.jpeg)

**Figure 7: Signal representation of audio data**


![WhatsApp Image 2023-02-12 at 3 27 41 PM](https://user-images.githubusercontent.com/92903308/218305114-2af2f95c-d4a6-42a2-8ba4-6e7a130bce60.jpeg)

**Figure 8: Cepstral Coefficients**

Then, generating the features based on the training set. Figure 9 shows the details of variables which were used to generate the features. Figure 10 represents the feature explorer that consists of 8 classes of audio data scattered in a 3D graph.

![WhatsApp Image 2023-02-12 at 3 27 41 PM (1)](https://user-images.githubusercontent.com/92903308/218305265-234d76fc-f560-423d-a9b8-a17ea8ed018b.jpeg)

**Figure 9: Generate features**

![WhatsApp Image 2023-02-12 at 3 27 41 PM (2)](https://user-images.githubusercontent.com/92903308/218305322-affc47b9-9aa2-491f-8edd-27ffe0c1210b.jpeg)

**Figure 10: Feature explorer**

Next, define the Neural Network settings by modifying the number of training cycles, learning rate and minimum confidence rating as shown in Figure 11. There are three options that enable us to build the Neural Network architecture. The architecture that was implemented is shown as Figure 13.

![WhatsApp Image 2023-02-12 at 3 27 42 PM](https://user-images.githubusercontent.com/92903308/218305387-61d5ed1e-ea8d-4c97-a83c-cff6065b8f57.jpeg)

**Figure 11: Neural Network settings
**

Input layer
	Input layer is the layer that consists of all the initial data for a neural network. 

Reshape layer
	Reshape layer is a common practice to overcome the limitation of Neural Network which only accept the fixed size data. Hence, with the existing reshape layer the data could be fed into the networks [2].

Pool layer
Pooling layer refers to pooling which is an approach to down sampling feature maps by summarizing the presence of features in patches of the feature map. Average pooling and max pooling are two common pooling methods that summarize the average presence of a feature and the most activated presence of a feature respectively [3].

Flatten layer
Flattening involves transforming the entire pooled feature map matrix into a single column which is then fed to the neural network for processing [4].

Dropout	
Dropout is referring to the ignoring units during the training phase. It is an approach to regulation of Neural Network which would reduce interdependent learning. [5]. It is a technique that prevents overfitting and provides a way of approximately combining exponentially many different neural network architectures efficiently [6]. Figure 12 shows the visualization of Dropout technique. 

<img width="253" alt="Screenshot 2023-02-12 182248" src="https://user-images.githubusercontent.com/92903308/218305471-0f736470-1bc9-4b8e-905d-5b9b86c12ac4.png">

**Figure 12: Dropout technique [6]**

![WhatsApp Image 2023-02-12 at 3 27 42 PM (1)](https://user-images.githubusercontent.com/92903308/218305516-446f2f07-2439-4a81-9155-91a8d6702dff.jpeg)

**Figure 13: Neural Network architecture
**

![WhatsApp Image 2023-02-12 at 3 27 43 PM](https://user-images.githubusercontent.com/92903308/218305550-6563d552-66a8-486c-8797-03a6ec5ac900.jpeg)

**Figure 14: Training process**

![WhatsApp Image 2023-02-12 at 3 27 41 PM (3)](https://user-images.githubusercontent.com/92903308/218305579-c3d557c5-dec0-43cf-9035-1154aa4258cd.jpeg)

**Figure 15: Training Performance**

Figure 14 shows the training process that is run by the model. Figure 15 shows the confusion matrix for all 8 classes of urban sounds. The top 3 classes that the model recognized were better for “Car Ambulance”, “Engine Idling” and “Drilling”, which are 100%, 100% and 71.4%. Overall, the training performance is as high as 58.5% accuracy with 2.01 loss as shown in Figure 15. 

Model testing

In model testing, 61 audio data from different classes are included to test the accuracy of the model. Figure 16 shows the result of model testing where the accuracy is . 

![WhatsApp Image 2023-02-12 at 3 27 43 PM (1)](https://user-images.githubusercontent.com/92903308/218305725-858fd0ee-345f-4e9b-9194-6c9e7aa64c33.jpeg)

**Figure 16: Test data**


Retrain Model

	In the retrain model, the model will be retrained with known parameters to improve the performance of the model and reduce loss. The result of the retrain model is shown as Figure 19. In addition, the accuracy of testing is improved after retraining the model. Figure 20 shows the result of testing, where the improvement is . 

![WhatsApp Image 2023-02-12 at 4 26 52 PM](https://user-images.githubusercontent.com/92903308/218305689-d5717a42-87fa-4fd7-8cba-239b1720bc9d.jpeg)

**Figure 17: Test data after retrain model**

The confusion matrix after retraining the model. After retraining the model, the model now performs better on recognizing “”, “”, “”, “” and “”.

Deployment
This section is to generate a source code and deploy it to the specified platform or device. The available options for the source code are as shown in Figure 18. Cube.MX CMSIS-PACK library is selected as the output source code. Then, a zip file will automatically be downloaded after it is finished built. 

![WhatsApp Image 2023-02-12 at 3 27 43 PM (2)](https://user-images.githubusercontent.com/92903308/218305804-7aa4f5b2-0274-4e05-b8c1-73574f650249.jpeg)

**Figure 18: Generating source code**

At last, the source code needs to be copied to the working directory of STMCubeIDE to perform real-time application with the Neural Network model.


## 8.0 References
1. Projects/Supervision (no date) Mun'im Zabidi. Available at: http://raden.fke.utm.my/projects (Accessed: January 7, 2023).
2. Smales, M. (2021) Sound classification using Deep Learning, Medium. Medium. Available at: https://mikesmales.medium.com/sound-classification-using-deep-learning-8bc2aa1990b7 (Accessed: January 7, 2023).
3. Zhang, Y. et al. (2018) Hello edge: Keyword spotting on microcontrollers, arXiv.org. Available at: https://arxiv.org/abs/1711.07128 (Accessed: January 7, 2023).

