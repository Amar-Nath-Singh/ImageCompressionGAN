# AUV Image Compression and Reconstruction System
![AUV Image Compression and Reconstruction System](https://github.com/Amar-Nath-Singh/ImageCompressionGAN/blob/main/demo_video.mp4)

## Objective
Design and implement a system that compresses images captured by AUVs (Autonomous Underwater Vehicles) for transmission and accurately reconstructs them at the surface with minimal error. The desired compression ratio should be at least 300 times, translating to a size of about 500-dimensional latent feature space. Mean Squared Error (MSE) loss between actual and reconstructed images will be considered as the metric for the competition.

## Context
To address the image compression challenge for AUVs, I have implemented a system comprising an AutoEncoder and a Generative Adversarial Network (GAN).

## AutoEncoder
The AutoEncoder serves as the primary component for image compression. It consists of three parts: Encoder, Bottleneck, and Decoder.

- **Encoder**: Compresses the input image into a 500-dimensional latent space, which reduces computational effort on the GPU, enhancing endurance.
- **Bottleneck**: Holds the encoded representation.
- **Decoder**: Reconstructs the image from the encoded representation. When an image is encoded, it returns a tensor of shape [500]. The Decoder returns a tensor of the original image shape and additional information from the Decoder as a skip connection with a shape of [256, 7, 7].

The AutoEncoder model is trained using the Adam optimizer with a learning rate 0.001 for 30 epochs. A learning rate step occurs at epoch 15 with a gamma of 0.8. Mean Squared Error (MSE) is utilized as the loss function.

### Encoder Architecture
- Input: Image of original size
- Convolutional layers
- Fully connected layers
- Output: Tensor of shape [500]

![image](https://github.com/user-attachments/assets/41ad5d94-e6ac-4a00-b047-cd33f7a4c3f6)
### BottleNeck
![image](https://github.com/user-attachments/assets/8aba9fa2-000a-49f1-a58e-4b977f007a22)

### Decoder Architecture
- Input: Tensor of shape [500]
- Fully connected layers
- Deconvolutional layers
- Skip connections from Encoder
- Output: Reconstructed image and additional information tensor of shape [256, 7, 7]
![image](https://github.com/user-attachments/assets/47d7a5a0-043e-46ed-a8b7-82e7d018905c)

### AutoEncoder Results
- Compression Ratio: 300x
- Latent Space Dimension: 500
- Loss Function: Mean Squared Error (MSE)

![image](https://github.com/user-attachments/assets/e0a0dca3-d58f-41e6-92e6-ad3c992ba8f3)


## Generative Adversarial Network (GAN)
A GAN-based approach is employed to enhance the quality of reconstructed images. The GAN consists of two components: Generator and Discriminator.

- **Generator**: Takes tensors of image size skip connections from the Decoder of the AutoEncoder and returns an enhanced tensor of the image size.
- **Discriminator**: Takes clear images and decoded images, returning patches of 14x14.
![image](https://github.com/user-attachments/assets/80545cd3-802b-4901-9019-a822b00e7f97)
![image](https://github.com/user-attachments/assets/3a2e28fc-4e89-4d66-9082-066a0989be50)

### Loss Functions
The GAN employs three loss functions:
1. **Adversarial Loss**: Calculated using MSE loss from the Discriminator.
2. **VGG Loss**: Utilizes a pre-trained VGG model to compute Perception Loss.
3. **L1 Loss**: Measures the difference between the image and its decoded counterpart.

The GAN model is trained using the Adam optimizer with a learning rate of 0.0001 for 40 epochs. A learning rate step occurs at epoch 10 with a gamma of 0.75.

### GAN Results
- Enhanced image quality
- Improved reconstruction accuracy

  ![image](https://github.com/user-attachments/assets/ce82e81c-7499-449b-b2c2-0b029d1bf42d)

