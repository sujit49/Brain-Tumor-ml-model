🧠 Brain Tumor Segmentation Using 3D U-Net📌 Project OverviewThis project implements an end-to-end deep learning pipeline for automated brain tumor segmentation from MRI scans. Utilizing a 3D U-Net architecture, the system is designed to perform voxel-wise binary classification to localize tumors effectively.The primary focus of this implementation is scalability and hardware efficiency. The pipeline has been optimized to run on mid-range hardware (limited RAM/GPU) while maintaining the architectural capacity to scale up for larger datasets and high-performance computing clusters.Key ObjectivesAutomate Diagnosis: Replace time-consuming manual annotation with rapid AI predictions.Hardware Optimization: Efficient data loading and processing for systems with limited memory.End-to-End Pipeline: From raw NIfTI file loading to final segmentation visualization.🗂 DatasetThe project utilizes the BraTS 2020 Dataset (Multimodal Brain Tumor Segmentation Challenge). The data consists of 3D MRI volumes in NIfTI format.Modalities included:FLAIR: Fluid Attenuated Inversion RecoveryT1: T1-weightedT1ce: T1-weighted with contrast enhancementT2: T2-weightedShutterstock⚠️ Hardware Note: To ensure this pipeline runs without crashing on consumer-grade hardware (e.g., 16GB RAM, 6GB VRAM), the training process utilizes reduced 3D patches and a subset of the total dataset.🏗 Model ArchitectureWe employ a 3D U-Net, a specialized convolutional neural network designed for volumetric biomedical image segmentation.Architecture Highlights:Encoder: 3D Convolutions followed by Max Pooling to capture context.Decoder: Transposed Convolutions for upsampling to restore spatial resolution.Skip Connections: Concatenates encoder feature maps with decoder maps to preserve fine-grained spatial details.Output Layer: Sigmoid activation for binary mask generation.The model is lightweight, containing fewer parameters than the standard U-Net to fit within a 12 GB RAM / GPU memory footprint.🔄 Preprocessing PipelineEfficient data handling is critical for 3D medical imaging. The pipeline uses nibabel for IO operations and custom generators for training.Volume Loading: Reading .nii or .nii.gz files.Normalization: Intensity normalization to standardize pixel values across scans.Resizing/Cropping: Volumes are cropped or resized to fixed dimensions (e.g., 128x128x64) to unify input shapes.Patch Generation: A custom data generator yields batches dynamically to prevent memory overflow during training.Splitting: Data is partitioned into Training, Validation, and Test sets.⚙ Training ConfigurationThe model is trained using a composite loss function to handle class imbalance (background vs. tumor).ParameterConfigurationLoss FunctionDice Loss + Binary Cross-EntropyOptimizerAdamBatch SizeSmall (optimized for memory constraints)EpochsConfigurable (Limited for demo, scalable for prod)Input Shape128 x 128 x 64 (3 Channels)💻 InstallationEnsure you have Python 3.8+ installed. Clone the repository and install the dependencies:Bash# Clone the repository
git clone https://github.com/yourusername/brain-tumor-segmentation.git
cd brain-tumor-segmentation

# Install dependencies
pip install tensorflow numpy nibabel matplotlib scikit-image
🚀 Usage1. Data SetupPlace your downloaded BraTS dataset files into the data/ directory following the structure below.2. Run the PipelineBash# Step 1: Preprocess the raw NIfTI files
python src/preprocessing.py

# Step 2: Train the 3D U-Net model
python src/train.py

# Step 3: Evaluate performance and generate visualizations
python src/visualize.py
3. Project StructurePlaintextproject/
│
├── data/
│   ├── images/       # Raw MRI scans (NIfTI)
│   └── masks/        # Ground truth segmentation masks
│
├── src/
│   ├── preprocessing.py   # Data loading, normalization, and generators
│   ├── model.py           # 3D U-Net architecture definition
│   ├── train.py           # Training loop and callbacks
│   └── visualize.py       # Inference and plotting scripts
│
├── outputs/
│   ├── predictions/       # Saved segmentation results
│   └── logs/              # Training history and model checkpoints
│
└── README.md
📊 Evaluation & ResultsThe model is evaluated using the Dice Coefficient (measuring overlap) and Binary Accuracy.Visualization Output:The visualize.py script generates side-by-side comparisons:Input: The raw MRI slice.Ground Truth: The expert-annotated mask.Prediction: The model's segmented output.Note: While the scaled-down model successfully detects tumor regions, boundary precision is limited by the reduced input resolution used for hardware efficiency.⚠ Limitations & Future WorkLimitationsFuture ImprovementsReduced Resolution: Training on smaller patches loses some global context.Full-Scale Training: Train on full-resolution volumes using multi-GPU setups.Modality Subset: Currently uses limited channels.All Modalities: Incorporate FLAIR, T1, T1ce, and T2 simultaneously.Basic U-Net: Standard architecture.Advanced Models: Implement Attention U-Net or nnU-Net for higher accuracy.No Post-Processing: Raw output usage.CRF/Morphology: Apply Conditional Random Fields or morphological cleaning to refine masks.
