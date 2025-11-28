Brain Tumor Segmentation Using 3D U-Net

This project implements a complete deep learning pipeline for brain tumor segmentation using 3D MRI scans from the BraTS dataset. The goal is to automatically segment tumor regions from volumetric medical images using a 3D U-Net architecture. Due to hardware limitations, the project was developed using reduced input sizes and fewer samples, but the pipeline is scalable for higher-end systems.

🔍 Overview

Brain tumor segmentation is a critical task in medical imaging and clinical diagnosis. Manual annotation of 3D MRI data is slow and requires specialist expertise. This project provides:

A preprocessing pipeline for 3D MRI volumes

A 3D U-Net model for voxel-level segmentation

Training and validation loops with data generators

Evaluation using Dice coefficient

Visualization of input slices, masks, and predictions across multiple slices

The project serves as a baseline framework that can be expanded, improved, and fully trained on powerful GPU hardware.

📂 Dataset: BraTS

This project uses the BraTS dataset, which includes multimodal MRI scans:

FLAIR

T1

T1ce

T2

Each sample includes a segmentation mask with tumor regions annotated.
For hardware practicality, the prototype uses:

Only FLAIR modality

A reduced subset of samples

Downscaled 3D volumes

🧼 Preprocessing

The preprocessing pipeline includes:

Loading .nii.gz NIfTI MRI volumes

Cropping or resizing to fixed input dimensions

Normalizing intensity values

Creating TensorFlow/Keras data generators

Splitting into training, validation, and test sets

This ensures memory-efficient loading and training.

🏗️ Model Architecture: 3D U-Net

The implemented 3D U-Net includes:

3D convolutional encoder

Bottleneck with deeper feature maps

3D transposed convolution decoder

Skip connections to preserve spatial features

Sigmoid activation for binary segmentation

The model is lightweight to accommodate limited GPU memory.

🏋️ Training

Training uses:

Dice + Binary Cross-Entropy loss

Adam optimizer

Small batch size (hardware constraint)

Reduced epochs

Real-time data loading

Despite limitations, the model learns the basic structure of tumor regions.

📊 Evaluation

Metrics include:

Dice coefficient

Binary accuracy

The project supports visualization of:

Input MRI slices

Ground truth masks

Prediction outputs (multiple slices or entire volume)

📈 Results

The model successfully performs basic tumor segmentation but with reduced accuracy due to:

Limited dataset size

Downscaled image resolution

Small batch size

Short training duration

The framework is fully functional and ready to scale up.

⚠️ Limitations

Because of hardware limitations (low VRAM, limited compute):

Only single-modality FLAIR was used

Full-resolution 3D volumes could not be processed

Model depth and batch size were reduced

Training was limited to fewer epochs

🚀 Future Improvements (With Better Hardware)

With a more powerful GPU, the following enhancements are possible:

Full-resolution BraTS input (240×240×155)

Multi-modal MRI (FLAIR, T1, T1ce, T2)

Larger and deeper 3D U-Net

Data augmentation

Longer training for better convergence

Advanced architectures (Attention U-Net, Residual U-Net, nnU-Net)

Post-processing to refine segmentation

These changes would significantly boost performance.

🛠️ Installation
pip install tensorflow numpy nibabel matplotlib scikit-image

▶️ Usage

Place MRI volumes and masks inside data/images/ and data/masks/.

Run the preprocessing script.

Train the model using train.py.

View predictions using visualize.py.

📁 Project Structure
project/
│
├── data/
│   ├── images/
│   └── masks/
│
├── src/
│   ├── preprocessing.py
│   ├── model.py
│   ├── train.py
│   └── visualize.py
│
├── outputs/
│   ├── logs/
│   └── predictions/
│
└── README.md
