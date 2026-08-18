# ResNet50-PetVision

## Cat and Dog Image Classification Using Transfer Learning

**ResNet50-PetVision** is a deep learning project that applies transfer learning to classify images into two categories: **cats and dogs**. The project uses the pretrained **ResNet50** convolutional neural network with ImageNet weights and adapts it to the target classification task.

The implementation explores two transfer learning strategies — **feature extraction** and **selective fine-tuning** — and compares them based on classification performance and training efficiency.

---

##  Project Overview

Deep learning models such as ResNet50 can learn powerful visual representations from large-scale datasets. Instead of training a complete CNN from the beginning, these learned representations can be reused for a new image classification problem.

In this project, ResNet50 is used as the pretrained backbone and a custom binary classification head is added for identifying cats and dogs.

The project follows two stages:

* **Feature Extraction:** The pretrained ResNet50 layers remain frozen while only the new classification layers are trained.
* **Fine-Tuning:** The final 30 layers of ResNet50 are unfrozen and trained with a smaller learning rate to adapt the pretrained features to the target dataset.

This type of workflow is commonly used when developing image classification systems because pretrained models can provide a strong starting point without requiring complete training from scratch. ([GitHub][1])

---

## Objectives

The project aims to:

* Implement transfer learning using ResNet50.
* Use ImageNet pretrained weights for image representation.
* Classify images into Cat and Dog categories.
* Compare feature extraction with selective fine-tuning.
* Measure training time for both approaches.
* Evaluate the trained model using multiple classification metrics.
* Analyze predictions using a confusion matrix.
* Identify the better-performing transfer learning strategy.
* Save the final trained model for further use.

---

## Dataset

The project uses a **Cats vs Dogs** image dataset containing two classes:

*  Cats
*  Dogs

The dataset is automatically acquired and organized by the notebook, so the image dataset does not need to be manually committed to the repository.

The images are divided approximately as follows:

| Split      | Proportion |
| ---------- | ---------: |
| Training   |        80% |
| Validation |        10% |
| Testing    |        10% |

### Dataset Structure

```text
dataset/
│
├── train/
│   ├── cats/
│   └── dogs/
│
├── val/
│   ├── cats/
│   └── dogs/
│
└── test/
    ├── cats/
    └── dogs/
```

---

## Data Preparation

Before training, the images undergo preprocessing to make them compatible with ResNet50.

The preprocessing pipeline includes:

* Resizing images to **224 × 224 pixels**
* Normalizing pixel values using `1/255`
* Horizontal flipping for training images
* Zoom augmentation for training images
* Keeping validation and test images free from augmentation
* Assigning binary labels to the two classes

---

## Model Architecture

The project uses **ResNet50 pretrained on ImageNet** as the feature extraction backbone.

The original classification layer is removed and replaced with a custom binary classification head.

```text
Input Image
     │
     ▼
Pretrained ResNet50
     │
     ▼
Global Average Pooling
     │
     ▼
Dense Layer
128 Units + ReLU
     │
     ▼
Dropout
0.3
     │
     ▼
Sigmoid Output
     │
     ▼
Cat / Dog
```

---

## Feature Extraction

In the first experiment, the ResNet50 backbone is completely frozen.

Only the newly added classification layers are trained.

```text
ResNet50 Backbone
      │
      │ Frozen
      ▼
Feature Representation
      │
      ▼
Custom Classification Head
      │
      ▼
Cat / Dog
```

This approach reduces the number of parameters that need to be updated during training.

---

##  Fine-Tuning

In the second experiment, the pretrained model is partially adapted to the Cats vs Dogs dataset.

The final **30 layers** of ResNet50 are made trainable while the earlier layers remain frozen.

A smaller learning rate is used during this stage so that the pretrained features are adjusted gradually.

```text
ResNet50
   │
   ├── Earlier Layers → Frozen
   │
   └── Final 30 Layers → Trainable
                │
                ▼
        Classification Head
                │
                ▼
             Cat / Dog
```

---

##  Training Configuration

| Parameter                        | Value               |
| -------------------------------- | ------------------- |
| Architecture                     | ResNet50            |
| Pretrained Dataset               | ImageNet            |
| Input Resolution                 | 224 × 224           |
| Batch Size                       | 32                  |
| Feature Extraction Epochs        | 5                   |
| Fine-Tuning Epochs               | 5                   |
| Feature Extraction Learning Rate | 0.001               |
| Fine-Tuning Learning Rate        | 0.00001             |
| Optimizer                        | Adam                |
| Loss Function                    | Binary Crossentropy |
| Output Activation                | Sigmoid             |

---

## Evaluation

Both approaches are evaluated using the same test dataset.

The following metrics are calculated:

* Accuracy
* Precision
* Recall
* F1-Score
* Training Time
* Confusion Matrix

Training and validation accuracy/loss curves are also generated to observe model learning behavior.

---

##  Performance Comparison

The experiment creates a benchmark comparing feature extraction and fine-tuning.

| Approach           |        Validation Accuracy |              Test Accuracy |              Training Time |
| ------------------ | -------------------------: | -------------------------: | -------------------------: |
| Feature Extraction | Generated during execution | Generated during execution | Generated during execution |
| Fine-Tuning        | Generated during execution | Generated during execution | Generated during execution |

The actual values are generated by the notebook after training.

---

##  Results

The project generates the following visualizations and outputs:

* Training accuracy curve
* Validation accuracy curve
* Training loss curve
* Validation loss curve
* Confusion matrix
* Classification report
* Precision
* Recall
* F1-score
* Accuracy comparison
* Training-time comparison
* Final benchmark table

---

##  Model Output

The trained model is saved in Keras format:

```text
models/
└── resnet50_final.keras
```

The notebook also determines which approach achieves the highest test accuracy.

---

##  Technologies

* Python
* TensorFlow
* Keras
* ResNet50
* NumPy
* Pandas
* Matplotlib
* Seaborn
* Scikit-learn
* Google Colab

---

## 🔄 Project Workflow

```text
Dataset Acquisition
        ↓
Dataset Organization
        ↓
Image Preprocessing
        ↓
Train / Validation / Test Split
        ↓
Pretrained ResNet50
        ↓
Feature Extraction
        ↓
Performance Evaluation
        ↓
Selective Fine-Tuning
        ↓
Performance Evaluation
        ↓
Benchmark Comparison
        ↓
Final Model Selection
        ↓
Model Saving
```

---

##  Conclusion

ResNet50-PetVision demonstrates the practical application of transfer learning for binary image classification.

By comparing feature extraction and selective fine-tuning, the project shows how pretrained visual representations can be reused and adapted instead of training a deep CNN entirely from scratch.

The final benchmark provides a practical comparison between **model performance and training efficiency**, helping identify the more suitable approach for the given Cats vs Dogs classification task.

[1]: https://github.com/guilhermedom/resnet50-transfer-learning-cats-and-dogs?utm_source=chatgpt.com "GitHub - guilhermedom/resnet50-transfer-learning-cats-and-dogs: Using TensorFlow API to transfer a ResNet-50 neural network and connect new fully connected layers to classify cats and dogs images. · GitHub"
