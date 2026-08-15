# FruitNet-V4X 🍎

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-orange.svg)](https://www.tensorflow.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**FruitNet-V4X** is a deep-learning-based fruit image classification project built with **TensorFlow/Keras** and **MobileNetV2 transfer learning**. The notebook classifies fruit images across fresh, rotten, and formalin-mixed categories and evaluates the model using **5-fold cross-validation**.

The current implementation works with a 15-class fruit image dataset containing Apple, Banana, Grape, Mango, and Orange samples under different quality/condition categories.

## Highlights

- MobileNetV2 pretrained on ImageNet
- Transfer learning with a frozen convolutional backbone
- 224 × 224 RGB image input
- Image normalization and augmentation
- Dense, Batch Normalization, Dropout, and feature-concatenation layers
- 5-fold cross-validation
- Classification reports and confusion matrices
- TPR, TNR, FPR, and FNR calculation
- Training/validation accuracy and loss visualization
- GPU-ready Kaggle notebook

## Model Pipeline

```text
Fruit Images
    │
    ▼
Resize to 224 × 224
    │
    ▼
Normalization / Data Augmentation
    │
    ▼
ImageNet-pretrained MobileNetV2
    │
    ▼
Feature Extraction
    │
    ▼
Dense + BatchNormalization + Dropout
    │
    ▼
Feature Concatenation
    │
    ▼
Dense Classification Layers
    │
    ▼
Softmax Output
    │
    ▼
15 Fruit Classes
```

## Dataset

The notebook currently expects the dataset at:

```python
dataset_dir = "/kaggle/input/fruite-dataset/Fruits Data"
```

The class labels are discovered automatically from the subdirectories inside `Fruits Data`.

A typical structure is:

```text
Fruits Data/
├── Apple Fresh/
├── Apple Rotten/
├── Apple Formalin-mixed/
├── Banana Fresh/
├── Banana Rotten/
├── Banana Formalin-mixed/
├── Grape Fresh/
├── Grape Rotten/
├── Grape Formalin-mixed/
├── Mango Fresh/
├── ...
└── Orange Formalin-mixed/
```

> If you run the notebook outside Kaggle or use a different dataset location, update `dataset_dir` accordingly.

## Data Preprocessing and Augmentation

Images are rescaled by `1/255`. The notebook also demonstrates augmentation using:

- Rotation up to 40°
- Width shift up to 20%
- Height shift up to 20%
- Shear transformation
- Zoom up to 20%
- Horizontal flipping
- Nearest-pixel filling

The primary image size is **224 × 224**, with a batch size of **32**.

## Training Configuration

| Parameter | Value |
|---|---|
| Backbone | MobileNetV2 |
| Pretrained weights | ImageNet |
| Input size | 224 × 224 × 3 |
| Optimizer | Adam |
| Learning rate | 0.0001 |
| Loss | Sparse Categorical Crossentropy |
| Batch size | 32 |
| Epochs | 20 per fold |
| Cross-validation | 5-fold |
| Random state | 42 |

## Results

The saved notebook output reports the following final validation accuracies:

| Fold | Validation Accuracy |
|---|---:|
| Fold 1 | 93.54% |
| Fold 2 | 95.51% |
| Fold 3 | 93.60% |
| Fold 4 | 94.22% |
| Fold 5 | 93.85% |
| **Average** | **94.14%** |

In addition to accuracy, the notebook calculates:

- Precision
- Recall
- F1-score
- Confusion matrix
- True Positive Rate (TPR)
- True Negative Rate (TNR)
- False Positive Rate (FPR)
- False Negative Rate (FNR)

## Repository Structure

```text
FruitNet-V4X/
├── FruitNet-V4X.ipynb
├── README.md
└── LICENSE
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/kowshir-bitto/FruitNet-V4X.git
cd FruitNet-V4X
```

### 2. Install the required packages

```bash
pip install numpy matplotlib scikit-learn tensorflow
```

### 3. Prepare the dataset

Place the fruit image folders in a directory and change:

```python
dataset_dir = "/path/to/Fruits Data"
```

If you are using Kaggle, attach the corresponding dataset to the notebook and keep the Kaggle input path.

### 4. Run the notebook

Open:

```text
FruitNet-V4X.ipynb
```

in **Kaggle**, **Jupyter Notebook**, **JupyterLab**, or **Google Colab**, update the dataset path if required, and run the cells in order.

## Requirements

The project uses:

```text
Python
TensorFlow / Keras
NumPy
Matplotlib
scikit-learn
```

The saved notebook metadata indicates a Python 3.11 environment and GPU-enabled Kaggle execution.

## Notes

- The dataset is not stored directly in this repository.
- Image classes are inferred from dataset subfolder names.
- Results may vary depending on dataset version, environment, TensorFlow version, random initialization, and hardware.
- A GPU is recommended for faster training.

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

## Author

**Abu Kowshir Bitto**

- GitHub: [@kowshir-bitto](https://github.com/kowshir-bitto)
- Website: [kowshirbitto.me](http://kowshirbitto.me/)
- Google Scholar: [Abu Kowshir Bitto](https://scholar.google.com/citations?hl=en&user=AO0dWsgAAAAJ&view_op=list_works&gmla=AJ1KiT30Ms5pY2DUl6pfWl4cwjlBOwygW_3wawpWiD_769YBbLX8_0rqv4MiIf05GjDe6xY81ApN7Gy1DfwYJCZu)
