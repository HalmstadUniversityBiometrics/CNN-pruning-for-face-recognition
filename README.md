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

**Abstract**
The widespread use of mobile devices for all kinds of transactions makes necessary reliable and real-time identity authentication, leading to the adoption of face recognition (FR) via the cameras embedded in such devices. Progress of deep Convolutional Neural Networks (CNNs) has provided substantial advances in FR. Nonetheless, the size of state-of-the-art architectures is unsuitable for mobile deployment, since they often encompass hundreds of megabytes and millions of parameters. We address this by studying methods for deep network compression applied to FR. In particular, we apply network pruning based on Taylor scores, where less important filters are removed iteratively. The method is tested on three networks based on the small SqueezeNet (1.24M parameters) and the popular MobileNetv2 (3.5M) and ResNet50 (23.5M) architectures. These have been selected to showcase the method on CNNs with different complexities and sizes. We observe that a substantial percentage of filters can be removed with minimal performance loss. Also, filters with the highest amount of output channels tend to be removed first, suggesting that high-dimensional spaces within popular CNNs are over-dimensioned.




