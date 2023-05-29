# SNN-MedMNIST
This project is implemented with [snnTorch](https://snntorch.readthedocs.io/en/latest/index.html) for the course "Introduction to Neuromorphic Computing" of National PhD in AI (Health and Life Sciences).
The main objective of the project is classifying chest x-ray images as pneumonia or normal. 
Because of the time and computational constrains, a simplified dataset is chosen, namely PneumoniaMNIST, a subset of [MedMNIST](https://medmnist.com/) which is a large-scale lightweight benchmark for medical image classification. 
The original dataset consists of 5,856 images; 1583 normal, 4273 pneumonia cases.
To make it balanced, the dataset is undersampled by randomly chosing 1583 pneumonia cases while keeping all the normal images.
Therefore, the undersampled dataset consists of 1583 normal and 1583 pneumonia cases, 3166 in total. 
The figure below shows some sample images belong to both classes.

![image](https://github.com/aksufatih/snn-medmnist/assets/49019174/47db3d95-a9cf-4b4d-9578-bf27f5b6998e)


All the images are gray level and they have a size of 28x28.
Since the dataset is already clean, no preprocessing is done. 
The only process done before feeding them to the network is spike encoding.
We applied rate coding to the images which transforms gray level intensities to spike frequencies. 
We used 20 time steps, chosen emprically, for all the experiments. 
The figure below shows an spikes of an example rate coded image.
For visualization purposes, 100 time steps are used. 
However, since the input image has a complex nature, the encoded spikes are not meaningful to human eye.

![image](https://github.com/aksufatih/snn-medmnist/assets/49019174/ae16ec41-2920-4ebb-be5f-bf8cfa82aee6)


We used a fairly simple network for this project, consists of 2 convolutional layers followed by max pooling layers each, and 1 fully connected layer in the end. 
The leaky integrate and fire neuron model is used as the neurons of the network. 
More info about the Leaky neuron can be found [here](https://snntorch.readthedocs.io/en/latest/snn.neurons_leaky.html).
You can find the overall architecture of the model and a brief description of Leaky neuron below.

![nn (5)](https://github.com/aksufatih/snn-medmnist/assets/49019174/2c9eff0c-f342-4bf6-a57c-728f1ace8a6a)
<img width="184" alt="Screenshot 2023-05-29 at 12 05 35" src="https://github.com/aksufatih/snn-medmnist/assets/49019174/1c64ffbe-f1ac-409c-9221-3866a5105dfb">

The network is trained for 20 epochs using Adam optimizer with a starting learning rate of 0.001. 
The learning rate is decreased by a factor of 0.1 at 10. epoch. 
Membrane potential decay rate is chosen as 0.6 in Leaky neurons. 
Spike rate cross entropy loss is used as loss function. 
Details of the loss function can be found [here](https://snntorch.readthedocs.io/en/latest/snntorch.functional.html#snntorch.functional.loss.ce_rate_loss).
The aim of CE rate loss is to increase the frequency of the correct class and decrease the frequency of the wrong class.
The video below shows an example output of an image with pneumonia. 
As seen in the video, the neuron pneumonia fires with a higher frequency than the other. 

https://github.com/aksufatih/snn-medmnist/assets/49019174/c34bdd05-a1d6-47c4-a226-056dc4b1dace


The result of the experiment is shown in the table below with 7 different metrics. Moreover, the loss graph is also depicted to show the training process of the model. The model achieves a 85% accuracy which indicates that it is a fairly good model. It should be noted that because of the time constrains, we didn't tune the hyperparameters in depth. It might be possible to reach higher results  by using a more complex model and tuning the parameters precisely. 

|      Model     | Accuracy | Sensitivity | Specificity | Precision | Recall | F1 Score | GMean |
|----------------|----------|-------------|-------------|-----------|--------|----------|-------|
| Proposed model |   0.853  |    0.880    |    0.825    |   0.834   |  0.880 |   0.857  | 0.852 |


<img src="https://github.com/aksufatih/snn-medmnist/assets/49019174/9441fbdb-ed57-4027-ba70-95fd4bfad41c" width="400" height="275">
