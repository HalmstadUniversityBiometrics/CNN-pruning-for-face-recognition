# Deep network pruning: A comparative study on CNNs in face recognition

This repository contains the models of the paper **Deep network pruning: A comparative study on CNNs in face recognition**, published at **Pattern Recognition Letters** in 2025 ([link](https://arxiv.org/abs/2405.18302) to paper in ArXiv) ([link](https://doi.org/10.1016/j.patrec.2025.01.023) to paper in the journal).

**Please consider citing the paper if you use in your research the models shared here:**
Fernando Alonso-Fernandez, Kevin Hernandez-Diaz, Jose Maria Buades Rubio, Prayag Tiwari, Josef Bigun,
Deep network pruning: A comparative study on CNNs in face recognition,
Pattern Recognition Letters,
2025,
ISSN 0167-8655,
https://doi.org/10.1016/j.patrec.2025.01.023.
(https://www.sciencedirect.com/science/article/pii/S0167865525000169)

# Summary

In the paper, we test a **CNN network pruning method based on Taylor scores** in the context of **face recognition**, where less important filters are removed iteratively. The method is tested on three networks based on the small **SqueezeNet** (1.24M parameters) and the popular **MobileNetv2** (3.5M) and **ResNet50** (23.5M) architectures. These have been selected to showcase the method on CNNs with different complexities and sizes. 

We observe that **a substantial percentage of filters can be removed with minimal performance loss**. Also, filters with the highest amount of output channels tend to be removed first, suggesting that **high-dimensional spaces within popular CNNs are over-dimensioned**.

# Implementation details

The models are trained on the MS-Celeb-1M and VGGFace2 databases (6.47M images in total). The networks have undergone a double fine-tuning, first over the MS1M-RetinaFace cleaned set (35k users/3.16M images, only users with more than 70 images), and then over VGGFace2 (9k users/3.31M images). Although VGG2 contains fewer users, it has more intra-class diversity due to more images per user. Due to this fact, the double fine-tuning strategy employed has shown increased performance compared to training the models only with one database, especially if it has few images per identity. This double fine-tuning implementation is suggested in the paper [VGGFace2: A dataset for recognising faces across pose and age](https://arxiv.org/abs/1710.08092).

The networks are trained for biometric identification using the soft-max function and ImageNet as initialization. The optimizer is SGDM (mini-batch=128, learning rate=0.01, 0.005, 0.001, and 0.0001, decreased when the validation loss plateaus). Two percent of images per user in the training set are set aside for validation. We apply horizontal random flip during training. We train with Matlab r2023b and use the ImageNet pre-trained model that comes with such release.

Afterwards, the pruning algorithm starts using the trained networks as input, which are pruned iteratively over the same training set. Given a mini-batch, the pruning method assigns an importance score to each filter of the network. At the end of each epoch, the scores of each filter are averaged over the mini-batches, and those with the smallest importance are removed. The resulting network can then be fine-tuned again to regain potential accuracy losses.

After training, feature vectors for biometric verification are extracted from the layer adjacent to the classification layer (i.e., the Global Average Pooling). These feature vectors are then used to conduct biometric verification experiments. 

# Provided models
  - We provide both the models after pruning, and after pruning + fine-tuning again. They are easily distinguishable in the folder names of the provided files. 

# Requirements
  - Matlab software (tested in r2023b). The models can be easily exported to **onnx models** using the Matlab function "exportONNXNetwork" (it is in our TO DO list to do so and upload the models to this repository).

# Pre-processing
  - **Input images must be of 113 x 113**.
  - We follow the tight crop of VGGFace2, with an extra 30% increase of the face bounding box, so some contextual information is added around the face. See attached examples to see how the input images should look like. The bounding box of VGG2 images is resized so the shortest side of the image has 129 pixels. Then, a 113x113 crop is taken.
  - The network is trained with images with some random displacement in horizontal and vertical dimensions (by taking a random 113x113 crop of the image during training), so it should be somehow tolerant to non-centered faces, althought it has not been tested (during testing, we only employ the center 113x113 crop of the bounding box). Bounding boxes provided with the VGG2 database are obtained using the MTCNN detector. See the VGGFace2 paper for more details.
