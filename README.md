# **EEG-Based Biometric Identification Using Deep Learning**

This project presents a deep learning system for identifying individuals based on EEG (Electroencephalography) signals recorded while processing Arabic speech.
A custom Convolutional Neural Network (CNN) architecture was developed to classify multichannel EEG signals into **12 different subjects** with high accuracy.

---

## **Project Objective**

Traditional authentication methods such as face recognition or fingerprints can be vulnerable to spoofing and unauthorized access.
EEG-based biometrics offers a more secure alternative because EEG signals are:

* Unique to every individual
* Extremely difficult to imitate
* Captured from real-time brain activity
* Resistant to spoofing attacks

This makes EEG-based identification a strong candidate for future identity verification systems.

---

## **Dataset Description**

The dataset used in training the model is:

**RIGHT_ONLY_full_dataset1.csv**

Each row in the dataset represents one EEG trial and includes:

| Column   | Description                                             |
| -------- | ------------------------------------------------------- |
| subject  | Subject ID (target class)                               |
| trial    | Trial number                                            |
| label    | Stimulation type (all samples are “Right”)              |
| v0–v1199 | EEG time-series values from 8 channels (≈9600 features) |

### **Final Input Shape for the CNN**

```
(samples, 8 channels, 1200 time steps, 1)
```

All signals were collected under “Right” stimulation, therefore no additional filtering was required.

---

## **Preprocessing Pipeline**

The preprocessing steps include:

1. Loading and inspecting raw EEG signals
2. Normalizing signal values
3. Reshaping each sample into the required 4D input format
4. Splitting the dataset into training and testing sets
5. Handling class distribution if necessary

---

## **Model Architecture**

A custom CNN architecture was designed specifically for multichannel EEG classification.
It includes the following main components:

* **Conv2D layers** for spatial–temporal feature extraction
* **DepthwiseConv2D** for channel-specific filtering
* **Residual Dense Blocks** for improved gradient flow
* **Batch Normalization** layers
* **Dropout** to reduce overfitting
* **Global Average Pooling**
* **Dense softmax layer (12 classes)**

This architecture captures both short-term and long-term EEG signal patterns effectively.

The architecture diagram is provided in:
`images/architecture.png`

---

## **Model Performance**

* **Accuracy:** ~86% on the test set
* Strong differentiation between subjects
* Robust performance despite EEG noise and variability

Performance visualizations (confusion matrix & training curves) are in:
`images/performance.png`

---

## **Training Details**

* **Loss Function:** SparseCategoricalCrossentropy
* **Optimizer:** Adam
* **Epochs:** 100 (with EarlyStopping)
* **Callbacks:**

  * ModelCheckpoint — saves best model
  * EarlyStopping — patience = 10

---

##  **Project Structure**


```
## Project Structure

project/
│
├── model.ipynb                # Training & evaluation notebook
├── RIGHT_ONLY_full_dataset1.csv
├── eeg_model.h5               # Saved trained model
├── README.md
└── images/                    # Architecture diagrams & plots
```

---

##  **How to Run**

1. Install required dependencies:

```
pip install tensorflow numpy pandas scikit-learn matplotlib
```

2. Open the training notebook:

```
model.ipynb
```

3. Run all cells to train, evaluate, and test the model.
4. The trained model is saved as:

```
eeg_model.h5
```

---

##  **Conclusion**

This project demonstrates the potential of EEG signals as a reliable biometric identification method.
With proper signal acquisition and deep learning techniques, brain-based identification can outperform many traditional authentication systems in security and uniqueness.

---
