# EE604_Course_Project
# Deep Fake Detection Using CNNs


---

## Abstract

Detecting manipulated facial images and videos is an increasingly important topic in digital media forensics. As advanced face synthesis and manipulation methods are made available, new types of fake face representations are being created which have raised significant concerns for their use in social media.  

The deepfake detection model proposed in this study is a dual-branch neural network architecture that combines **EfficientNet** (a pre-trained convolutional neural network) with a handcrafted feature extraction branch. This dual-branch structure aims to enhance detection performance by leveraging both high-level feature representations from a deep learning model and specific handcrafted statistical features, creating a more comprehensive approach to identify deepfake images.  

Our model was trained and evaluated on a comprehensive dataset of real and deepfake photos, achieving an accuracy of **73%**, thus providing a robust approach for reliable deepfake detection.

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Proposed Method](#proposed-method)  
   - [EfficientNet Branch](#efficientnet-branch)  
   - [Handcrafted Feature Branch](#handcrafted-feature-branch)  
3. [Feature Fusion and Classification](#feature-fusion-and-classification)  
4. [Results](#results)  
5. [Appendix](#appendix)  

---

## 1. Introduction

With the rapid growth of deepfake technology, synthetic media can now be generated with astonishing realism using readily available tools and resources, often on consumer-grade hardware. This ease of production has made deepfakes a significant challenge in various domains, from social media misinformation to identity theft.  

The novelty of this idea lies in the detection method of merging **deep learning** and **handcrafted feature extraction** in a unified architecture. While typical models rely solely on CNNs for feature extraction, our approach incorporates specific handcrafted features (e.g., **color histograms, edge, and texture information**) alongside deep network outputs to capture additional, nuanced image characteristics. This combined approach aims to improve detection accuracy and robustness, especially in scenarios where subtle visual artifacts are difficult for standard CNNs to detect alone.

---

## 2. Proposed Method

### 2.1. EfficientNet Branch

#### 2.1.1 Input and Preprocessing

- Input: RGB images with a shape of 224x224 pixels (3 color channels).  
- Preprocessing: Normalizes pixel values between 0 and 1 to improve training stability.  

#### 2.1.2 Feature Extraction

- Uses **EfficientNetB0**, pre-trained on ImageNet.  
- EfficientNet serves as a feature extractor by outputting a feature map with high-level abstractions such as textures and spatial relationships.  

#### 2.1.3 Post-Extraction Processing

- **Local Binary Patterns (LBP):** Encodes local texture features, generating a 10-bin histogram for each image.  

---

### 2.2. Handcrafted Feature Branch

#### 2.2.1 Features Extracted

1. **Color Histogram Features (216 dimensions):** Captures color distribution using 6 bins per channel.  
2. **Edge Features (16 dimensions):** Derived using Canny edge detection.  
3. **Local Binary Patterns (LBP):** Encodes texture changes using 10-bin histograms.  
4. **Statistical Features (20 dimensions):** Calculates global and regional statistics, including mean, median, and percentiles.  

#### 2.2.2 Feature Vector Construction

The extracted features (262 dimensions) are processed using dense layers with **ReLU activation** and **dropout** for refinement.

---

## 3. Feature Fusion and Classification

- The outputs from EfficientNet and the handcrafted feature branch are **concatenated**.  
- The concatenated vector is passed through dense layers with **batch normalization** and **dropout** to avoid overfitting.  
- **Sigmoid activation** is used in the output layer for binary classification.  

---

## 4. Results

- **Test Accuracy:** Achieved 73% accuracy.  
- Fine-tuning of EfficientNetB0 contributed significantly to detection performance.  
- Challenges included optimizing handcrafted feature extraction and tuning hyperparameters.  

---

## 5. Appendix

- **GitHub Repository:** [EE604 Course Project](https://github.com/AyushInamdar/EE604_Course_Project/blob/main/DualBranch.ipynb)  
- **Dataset Link:** [Google Drive](https://drive.google.com/drive/folders/16TXEcnqaxg9kDgY_oHoTaLUXgkZtW2_i?usp=sharing)  

---

*Note: Additional figures and tables referenced in the report can be included as required.*
