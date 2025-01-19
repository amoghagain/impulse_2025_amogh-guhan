
# EEG Signal Classification Project  
**Impulse 2025 Hackathon - Biomedical Signal Processing**

## Overview  
This project focuses on developing a robust model for classifying Electroencephalogram (EEG) seizure types from signals. The model integrates explainability techniques to promote clinical trust in hospital settings. The classification task involves distinguishing between four classes of EEG signals:  
- **Normal**  
- **Complex Partial Seizures**  
- **Electrographic Seizures**  
- **Video-detected Seizures with no visual change over the EEG**  

---

## Features and Tasks  

### 1. **Basic Analysis**  
- **Visualization**: EEG signals for all 19 channels.  
- **Time Domain Metrics**:  
  - Mean  
  - Zero Crossing Rate  
  - Range  
  - Energy  
  - RMS  
  - Variance  

### 2. **Frequency Domain Feature Extraction**  
- Fourier Transform implementation  
- Wavelet Decomposition (4 levels)  
- Spectrogram generation and analysis  
- Channel-wise analysis of coefficients  

### 3. **Baseline Model**  
- **Feature Set**: Fourier features + Zero Crossing Rate  
- **Classifier**: SVM  
- **Performance Metrics**:  
  - Classification Report  
  - ROC AUC Score  
  - Balanced Accuracy  

### 4. **Advanced Model**  
- Enhanced feature extraction methods  
- Deep learning implementation. A convolutional neural network was implemented using Conv1D layers. The EEG signals were fed to the network directly. An accuracy of ~95% was achieved  
- XGBoost model - An XGBoost model was implemented on extracted features, achieving an accuracy of ~97%. 
- Performance evaluation on validation and test sets  

---

## Model Interpretability and Robustness Analysis  

### **SHAP Analysis for XGBoost Model**  
To ensure transparency and interpretability of the XGBoost model, SHAP (SHapley Additive exPlanations) was employed to analyze feature contributions for predictions.  

#### Key Steps:  
1. **Force Plots for Feature Contribution**:  
   - Visualized dominant features influencing each prediction.  
2. **Identifying Key Features**:  
   - Top 3 influential features for each prediction were identified using SHAP values.  
3. **Feature Masking and Re-Evaluation**:  
   - The top 3 features were masked, and predictions were re-evaluated.  
   - Accuracy dropped marginally from **97% to 94%**, showcasing model robustness.  

#### Conclusion:  
The SHAP analysis confirmed that the XGBoost model is not overly dependent on a small subset of features, demonstrating its generalizability and reliability for complex EEG data.

---

## Signal Denoising  

### **Overview**  
Various filtering techniques were applied to noisy EEG data to improve signal quality. Post-filtering, **Peak Signal-to-Noise Ratio (PSNR)** values were calculated to quantify the improvement.  

#### **Filters Applied**  
1. **Butterworth Filter**:  
   - Removes noise outside a specified frequency range (e.g., 0.5–50 Hz).  
   - Effective at eliminating low-frequency drift and high-frequency artifacts.  

2. **Savitzky-Golay Filter**:  
   - Smoothens signals while preserving waveform shapes.  
   - Reduced high-frequency noise and maintained transient features.  

3. **Notch Filter**:  
   - Eliminates narrowband noise like powerline interference (50/60 Hz).  
   - Efficiently removed periodic noise with minimal distortion.  

#### **Evaluation**  
- **PSNR Values**:  
  - Objectively measured signal improvement.  
  - Higher PSNR values indicated better noise reduction with minimal distortion.  

- **Summary of Results**:  
  - *Butterworth Filter*: Best for overall band-limited noise removal.  
  - *Savitzky-Golay Filter*: Preserved signal morphology effectively.  
  - *Notch Filter*: Most effective at eliminating powerline interference.  

#### **Conclusion**  
The filtering techniques significantly enhanced EEG signal quality. PSNR values validated their effectiveness, making the filtered signals suitable for downstream tasks like feature extraction and machine learning.

---

## Generative Modeling  

### **Variational Autoencoder (VAE)**  
A Variational Autoencoder (VAE) was implemented for EEG signal classification and synthetic data generation. The model handles all four classes of EEG signals.  

#### **Features**  
- Residual block-based VAE architecture  
- Focal loss with class weighting  
- Advanced data augmentation techniques  
- Synthetic data generation  
- Comprehensive visualization tools  
