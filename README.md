# HAR-Attnsense

This project is be base on the paper ”AttnSense: Multi-level Attention Mechanism For Multimodal Human Activity Recognition” by Ma, Li, Zhang, Gao, Lu.

The preprocess was done on PAMAP2 dataset. We implemented the preprocess according to the steps described in the paper.
The steps are:
1. Calculating the energy content (norm) separately for each sensor.
2. Normalization for each feature.
3. Augmented data. Increasing the number of samples by adding normal noise to the original data.
4. Creating spectrogram with Fast Fourier Transform for every 200 samples (2 second) with 25% overlap.
5. Taking 5 timesteps sequences as one instance for the data loader (N=5).


The network is built of several sections:
1. Individual convolutional layers.
2. Attention - between different modalities for each timestep.
3. GRU.
4. Attention - between different timesteps.
5. Fully connected layer + Softmax.

Innovative notebook
RNN and GRU are mainly used for sequential processing over time which takes a lot of resources and time.
The innovative part is to replace the GRU layer in the network into stacked self-attention layers which will produce positional embedding.
The idea came from the domain of NLP as introduced in the paper ’Attention is all you need’.
The motivation behind this change is to improve the calculation speed by better utilization of the hardware and parallel calculation which is impossible in RNNs.

The innovative network is built of several sections:
1. Individual convolutional layers.
2. Additive Attention - between different modalities for each timestep.
3. 3 stacked Encoder layers.
4. Additive Attention - between different timesteps.
5. Fully connected layer + Softmax.
