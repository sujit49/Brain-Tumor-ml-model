🧠 Brain Tumor Segmentation Using 3D U-Net

This project implements an end-to-end deep learning pipeline for automated brain tumor segmentation from MRI scans using a 3D U-Net architecture. It focuses on scalable, hardware-efficient processing while providing accurate tumor localization.

📌 Project Overview

Brain tumor segmentation is a crucial task in medical imaging, enabling faster and more accurate diagnosis. Manual annotation is time-consuming and requires expert knowledge.

This project develops a pipeline capable of:

Loading and preprocessing 3D MRI volumes

Normalizing and resizing the data

Training a 3D U-Net for voxel-wise tumor segmentation

Evaluating predictions using the Dice coefficient metric

Visualizing input, ground truth, and model predictions

The project has been scaled down to fit mid-range hardware, but the architecture is ready to be scaled for larger datasets and better GPUs.

🗂 Dataset

The project uses the BraTS 2020 Dataset, which includes multimodal MRI scans:

FLAIR

T1

T1ce

T2

Each scan includes a corresponding tumor segmentation mask.

Note: For hardware efficiency, training uses reduced 3D patches and a subset of the dataset. This ensures the pipeline works without crashing on systems with limited RAM or GPU memory.

4️⃣ Provide instructions for users to download datasets

Instead of including kaggle.json, in your README, tell users how to create their own API key:

**Dataset Download Instructions**

1. Create a Kaggle account.
2. Go to Account → API → Create New API Token.
3. Place the downloaded `kaggle.json` file in your working directory.
4. Run the provided preprocessing script to load data.

🔄 Preprocessing

Steps included in preprocessing:

Loading NIfTI files using nibabel

Intensity normalization of MRI volumes

Resizing/cropping to fixed dimensions (e.g., 128x128x64)

Patch-based data generator to load batches dynamically

Splitting dataset into training, validation, and test sets

These steps reduce memory usage and allow for real-time training with limited hardware.

🏗 Model Architecture

A 3D U-Net is used for segmentation:

Encoder with 3D convolutions and max pooling

Decoder with transposed convolutions for upsampling

Skip connections to preserve spatial information

Sigmoid activation for binary segmentation

The model is lightweight to fit within 12 GB RAM / GPU memory constraints.

⚙ Training

Training configuration:

Loss: Dice loss + Binary Cross-Entropy

Optimizer: Adam

Batch size: small, to prevent memory overflow

Epochs: limited (can increase with better hardware)

Real-time data feeding using custom patch generators

📊 Evaluation

Metrics used:

Dice coefficient

Binary accuracy

Visualization includes:

Input MRI slices

Ground truth tumor masks

Predicted tumor masks

Multiple slice and multi-patient comparisons

📈 Results

The scaled-down model is able to detect tumor regions.

Accuracy is limited due to smaller input size, reduced batch size, and fewer training samples.

The pipeline is fully functional and ready for scaling to larger datasets.

⚠ Limitations & Improvements

Current limitations:

Training uses reduced patch sizes and dataset subset

Limited batch size due to hardware

Single-modality or fewer channels

Potential improvements with better hardware:

Use full-resolution volumes

Train on all four MRI modalities (FLAIR, T1, T1ce, T2)

Implement deeper or attention-based networks (Attention U-Net, nnU-Net)

Apply data augmentation for better generalization

Post-processing using CRFs or morphological operations

💻 Installation
# Python 3.8 or higher
pip install tensorflow numpy nibabel matplotlib scikit-image

🚀 Usage

Place dataset in data/ folder

Run preprocessing script: preprocessing.py

Train model: train.py

Evaluate and visualize results: visualize.py

📁 Project Structure
project/
│
├── data/
│   ├── images/       # MRI scans
│   └── masks/        # Tumor segmentation masks
│
├── src/
│   ├── preprocessing.py
│   ├── model.py
│   ├── train.py
│   └── visualize.py
│
├── outputs/
│   ├── predictions/
│   └── logs/
│
└── README.md

🔮 Future Work

Full-scale training on larger datasets

Multi-class tumor segmentation (enhancing tumor, edema, necrosis)

Integration with clinical pipelines

3D volume visualization in interactive format
