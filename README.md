Brain Tumor Segmentation Using 3D U-Net

This project focuses on automated brain tumor segmentation using MRI scans from the BraTS dataset. It uses a 3D U-Net architecture to segment tumor regions from multimodal MRI volumes. Due to hardware limitations, the project is currently scaled down but designed so that performance can significantly improve on a higher-end system.

Project Overview

Brain tumor segmentation is a critical task in medical imaging. Manual annotation is time-consuming and requires expert knowledge. This project develops an end-to-end deep learning pipeline capable of:

Loading and preprocessing MRI volumes

Normalizing and resizing 3D medical images

Training a 3D U-Net for voxel-wise segmentation

Evaluating predictions using Dice coefficient

Visualizing input slices, ground truth, and model outputs

The primary objective is to create a baseline segmentation model that can be improved and scaled up with better hardware.

Dataset

The project uses the BraTS (Brain Tumor Segmentation) dataset, which contains multimodal MRI scans including:

FLAIR

T1

T1ce

T2

Each scan includes a corresponding mask for tumor segmentation.
For hardware reasons, only one modality (FLAIR) and a reduced number of samples were used during development.

Preprocessing

Key preprocessing steps:

Loading NIfTI files

Cropping or resizing volumes to fixed dimensions

Intensity normalization

Creating data generators for efficient training

Splitting data into training, validation, and testing sets

Model Architecture

A modified 3D U-Net is used:

Encoder with 3D convolutions and max pooling

Decoder with transposed convolutions for upsampling

Skip connections to preserve spatial information

Sigmoid output for binary segmentation

Training

Training includes:

Binary cross-entropy and Dice loss

Adam optimizer

Batch size adjusted due to GPU limitations

Real-time data loading via generators

Because of hardware constraints, the model is trained on reduced 3D dimensions and fewer samples, resulting in lower accuracy but a working prototype pipeline.

Evaluation

Metrics used:

Dice coefficient

Binary accuracy

Visual inspection of slices

Visualization code allows comparison of:

Input MRI slice

Ground truth mask

Predicted segmentation

Multiple slice visualization across the volume is also supported.

Results

The prototype model is able to detect tumor regions but with limited precision due to:

Small dataset portion

Low input resolution

Limited training time

Restricted batch size

However, the pipeline works end-to-end and is ready for scaling.

Limitations and Improvements

With better GPU hardware, the following improvements can be implemented:

Using full-resolution BraTS volumes

Training on all MRI modalities

Larger batch sizes and deeper networks

More epochs for better convergence

Data augmentation

Advanced architectures like Attention U-Net or nnU-Net

Post-processing methods such as CRFs or morphological operations

Installation

Python 3.8 or higher recommended. Install dependencies:

pip install tensorflow numpy nibabel matplotlib scikit-image

Usage

Place dataset in the specified directory

Run preprocessing script

Train the model

Visualize predictions

Evaluate performance

Folder Structure
project/
  data/
      images/
      masks/
  src/
      preprocessing.py
      model.py
      train.py
      visualize.py
  outputs/
      predictions/
      logs/
README.md
