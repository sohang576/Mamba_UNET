# Mamba-UNet: Efficient Building Segmentation from Aerial Images

This repository presents **Mamba-UNet**, a deep learning architecture for **building footprint extraction from high-resolution aerial images**.

The model integrates **Selective State Space Models (Mamba)** with the **U-Net encoder–decoder architecture** to capture both **local spatial details and long-range global relationships** while maintaining **linear computational complexity**.

The proposed method achieves strong segmentation accuracy while significantly reducing computational cost compared to CNN and Transformer-based models.

---

# Overview

Accurate building footprint extraction from aerial or satellite imagery is critical for several real-world applications:

- Urban planning
- Disaster damage assessment
- Geographic Information Systems (GIS)
- Infrastructure monitoring
- Smart city development

Traditional deep learning approaches typically rely on:

• CNN-based models (U-Net, SegNet)  
• Transformer-based architectures (SegFormer, Swin-UNet)

However:

- CNN models struggle with **global context understanding**
- Transformer models are **computationally expensive**

To address these limitations, this work introduces **Mamba-UNet**, which combines:

- Efficient **state space sequence modeling**
- Spatial feature extraction from **U-Net**

This results in **high segmentation accuracy with significantly reduced computational cost**.

---

# Key Contributions

1️⃣ **Hybrid Architecture**

Proposed **Mamba-UNet**, combining:

- U-Net encoder–decoder structure
- Mamba State Space Blocks

2️⃣ **Global Context Modeling**

Mamba modules capture **long-range spatial relationships** across the image.

3️⃣ **Improved Efficiency**

The architecture achieves:

- **70% reduction in computational cost**
- Only **9.87M parameters**

4️⃣ **Strong Segmentation Performance**

The model achieves high **IoU and Dice scores** on benchmark building segmentation datasets.

---

# Model Architecture

The proposed architecture follows a **U-Net style encoder-decoder design** enhanced with **Mamba blocks**.

Pipeline:

```
Input Image
     ↓
Encoder (Conv Blocks + Mamba Blocks)
     ↓
Bottleneck Layer
     ↓
Decoder (Upsampling + Skip Connections)
     ↓
Segmentation Output
```

### Encoder

The encoder extracts hierarchical image features using:

- Convolution layers
- Batch normalization
- ReLU activation
- Max pooling

A **Mamba block** is inserted to capture global relationships.

---

### Mamba Block

The Mamba block is based on **Selective State Space Models (SSM)**.

It contains the following steps:

1️⃣ Input Projection  
2️⃣ Local Spatial Convolution  
3️⃣ Selective Feature Gating  
4️⃣ Global Dependency Modeling using SSM  
5️⃣ Residual Feature Fusion

This allows the model to combine:

- **Local spatial features (CNN)**
- **Long-range dependencies (State Space Models)**

---

### Decoder

The decoder reconstructs the segmentation map using:

- Transposed convolutions (upsampling)
- Skip connections from encoder
- Convolution refinement layers

Skip connections help preserve **fine boundary information**.

---

# Dataset

The model was evaluated on two widely used building segmentation datasets.

## WHU Building Dataset

- High-resolution aerial images
- 0.3m spatial resolution
- 8,188 image tiles
- Image size: **512 × 512**

Contains diverse urban structures and complex building layouts.

📷 **Dataset Example**

[INSERT WHU DATASET SAMPLE IMAGE HERE]

---

## Massachusetts Building Dataset

- High-resolution aerial images
- 1m spatial resolution
- Image size: **1500 × 1500**

Images are divided into smaller **224×224 patches** for training.

📷 **Dataset Example**

[INSERT MASSACHUSETTS DATASET SAMPLE IMAGE HERE]

---

# Data Preprocessing

Several preprocessing steps were applied before training:

• RGB masks converted to binary building masks  
• Image resizing to **224 × 224**  
• Random horizontal flipping  
• Image normalization  

These steps help improve **generalization and training stability**.

---

# Training Configuration

The model was implemented using **PyTorch**.

Training environment:

- Platform: Kaggle
- GPUs: **Dual NVIDIA T4**
- Epochs: **30**

Hyperparameters:

| Parameter | Value |
|----------|------|
Learning Rate | 1e-4  
Optimizer | Adam  
Batch Size | 16 (WHU) / 8 (Massachusetts)  
Weight Decay | 5e-4  

Loss Function:

```
Total Loss = 0.5 * BCE + 0.5 * Dice Loss
```

This balances:

- Pixel accuracy
- Region overlap

---

# Evaluation Metrics

Model performance was evaluated using:

- Intersection over Union (IoU)
- Dice Score
- Precision
- Recall
- F1 Score
- Accuracy

---

# Results

## Massachusetts Building Dataset

| Metric | Score |
|------|------|
Precision | 88.61% |
Recall | 84.33% |
F1 Score | 86.17% |
IoU | 68.94% |

---

## WHU Building Dataset

| Metric | Score |
|------|------|
Precision | 94.39% |
Recall | 93.01% |
F1 Score | 93.67% |
IoU | 89.04% |

---

# Segmentation Results

Example predictions produced by **Mamba-UNet**.

### Massachusetts Dataset Results

[INSERT SEGMENTATION RESULTS FIGURE HERE]

---

### WHU Dataset Results

[INSERT SEGMENTATION RESULTS FIGURE HERE]

---

# Training Curves

### Training Loss

[INSERT TRAINING LOSS GRAPH HERE]

---

### Accuracy / IoU Curve

[INSERT TRAINING ACCURACY GRAPH HERE]

---

# Computational Efficiency

Compared with popular architectures:

| Model | Parameters | GFLOPs |
|------|------|------|
U-Net | 31M | 120 |
SegNet | 29.4M | 108 |
Attention U-Net | 31.39M | 42.76 |
Residual U-Net | 35.92M | 52.25 |
**Mamba-UNet (Proposed)** | **9.88M** | **10.90** |

Additional metrics:

- Inference time: **8.68 ms**
- Throughput: **121 samples/sec**

This demonstrates that **Mamba-UNet provides strong accuracy while being computationally efficient**.

---

# Statistical Validation

To verify the robustness of results:

- Experiments repeated **5 times with different seeds**
- **Paired t-test** applied on IoU scores

Results showed **p-values < 0.01**, confirming statistical significance at **99% confidence**.

---

# Advantages of Mamba-UNet

• Captures long-range dependencies efficiently  
• Lower computational cost than Transformers  
• Better boundary detection  
• Improved segmentation of small buildings  

---

# Future Work

Future improvements may include:

- Multi-class urban object segmentation
- Temporal change detection
- Real-time remote sensing pipelines
- Integration with lightweight attention mechanisms

---

# Authors

**Sohang Debnath**  
School of Computer Engineering  
KIIT Deemed to be University  

Co-authors:

- Mainak Bandyopadhyay  
- Prasenjit Maiti  

---

# Citation

If you use this work, please cite:

```
Bandyopadhyay, M., Debnath, S., Maiti, P.
Efficient Building Segmentation from Aerial Images using MAMBA State Space Modeling.
```

---

# License

This project is intended for **research and academic purposes**.
