# SNN-MedMNIST
This project is implemented for the course "Introduction to Neuromorphic Computing" of National PhD in AI (Health and Life Sciences).
The main objective of the project is classifying chest x-ray images as pneumonia or normal. 
Because of the time and computational constrains, a simplified dataset is chosen, namely PneumoniaMNIST, a subset of [MedMNIST](https://medmnist.com/) which is a large-scale lightweight benchmark for medical image classification. 
The original dataset consists of 5,856 images; 1583 normal, 4273 pneumonia cases.
To make it balanced, the dataset is undersampled by randomly chosing 1583 pneumonia cases while keeping all the normal images.
Therefore, the undersampled dataset consists of 1583 normal and 1583 pneumonia cases, 3166 in total. 
The figure below shows some sample images belong to both classes.

![image](https://github.com/aksufatih/snn-medmnist/assets/49019174/91dda72f-11ac-4d43-92e4-df9c7a252b19)

All the images are gray level and they have a size of 28x28.
Since the dataset is already clean, no preprocessing is done. 
The only process done before feeding them to the network is spike encoding.
We applied rate coding to the images which transforms gray level intensities to spike frequencies. 
We used 20 time steps, chosen emprically, for all the experiments. 
The figure below shows an example rate coded image.
For visualization purposes, 100 time steps are used. 
However, since the input image has a complex nature, the encoded spikes are not meaningful to human eye.

![image](https://github.com/aksufatih/snn-medmnist/assets/49019174/6cd2e96b-1ea5-4ed4-868c-dc32eeac2337)

We used a fairly simple network for this project, consists of 2 convolutional layers followed by max pooling layers each, and 1 fully connected layer in the end. 
The leaky integrate and fire neuron model is used as the neurons of the network. 
More info about the Leaky neuron can be found [here](https://snntorch.readthedocs.io/en/latest/snn.neurons_leaky.html).
You can find the overall architecture of the model and a brief description of Leaky neuron below.

![nn (5)](https://github.com/aksufatih/snn-medmnist/assets/49019174/586234e7-3ffa-4ea9-ac58-b645d55e6ff3)
<img width="184" alt="Screenshot 2023-05-29 at 12 05 35" src="https://github.com/aksufatih/snn-medmnist/assets/49019174/82ce63c1-ae8c-40b1-a468-19c2379ffd0e">




