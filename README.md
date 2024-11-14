# PoseMaster-Dynamic-Person-Repose-and-Face-Transformation
PoseMorphAI is a comprehensive pipeline built using ComfyUI and Stable Diffusion, designed to reposition people in images, modify their facial features, and change their clothes seamlessly. This solution leverages advanced pose estimation, facial conditioning, image generation, and detail refinement modules for high-quality output.

![result](https://github.com/Toldblog/PoseMaster-Dynamic-Person-Repose-and-Face-Transformation/blob/main/output.jpg)

## Overview
PoseMaster is an advanced pipeline for transforming images of people by reposing them, changing their facial features, and modifying their clothes. The project uses state-of-the-art models from ComfyUI and Stable Diffusion to deliver realistic transformations. Key functionalities include:

- Dynamic reposing based on a target pose image.
- Facial feature modification using a reference image.
- Clothes changing through segmentation masks and reference images.
- This is achieved by leveraging a series of pre-trained models and a modular approach to processing input data, image conditioning, and output generation.

## Requirements
To run PoseMaster, you'll need the following dependencies:

- Python 3.7+
- PyTorch
- TorchVision
- Pillow (PIL)
- Numpy
- ComfyUI and its related modules
- Pre-trained models for ControlNet, CLIP, IP-Adapters, FreeU-V2,...

## Setup and Installation
Clone this repository and navigate to the project directory:

```
git clone <your-repository-url>
cd <your-repository-directory>
```

Install the required Python packages as described in the Requirements section.

Ensure you have the necessary pre-trained models and place them in the appropriate directories. Some example models include:

- vae-ft-mse-840000-ema-pruned.safetensors
- realdream.safetensors
- control_v11p_sd15_openpose.pth
- and more...

Modify any paths in the code to match your local setup if needed.

## Project Workflow

### Input Loading
PoseMaster starts by loading input images, which include:

- Pose Images: Define the target body positioning.
- Face Images: Used to condition facial features.
- Clothes Images: Provide reference for clothing transformation.

### Model Initialization
The pipeline initializes several models using ComfyUI nodes, including:

- VAE Loader: Loads a Variational Autoencoder (VAE) for image encoding and decoding.
- Checkpoint Loader: Loads the main Stable Diffusion checkpoint.
- CLIP Text Encoder: Encodes text prompts for conditioning image generation.
- ControlNet Loader: Applies ControlNet conditioning for pose and other inputs.
- IP-Adapter Loader: Integrates visual and textual embeddings for image conditioning.
- Detector & SAM Model Loader: Used for segmentation and detection.
  
### Pose and Face Processing
1. Pose Estimation:
The pose of the input image is estimated using Dwpose models to generate key points for the body, face, and hands.
2. Face Conditioning:
The face image is processed using the IP-Adapter, which combines visual and textual embeddings to condition image generation.

### Image Generation and Refinement
1. ControlNet Conditioning:
The pipeline applies ControlNet conditioning based on the pose, facial features, and other inputs.
2. FreeU-V2 Processing:
Patch-based image processing is performed to enhance image details.
3. Sampling and Upscaling:
Neural network-based latent sampling and upscaling are performed for high-quality image generation.

#### Clothes Replacement

1. Segmentation:
GroundingDINO and SAM models are used to segment specific areas, such as clothes, in the input image.
2. Clothes Transformation:
The segmented areas are modified using a reference clothes image with CAT-VTON.

### Output Generation
The final image is decoded from the latent space, refined using detailers, and saved as output.

# License
This project is licensed under the MIT License. See the LICENSE file for more details.








