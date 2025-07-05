# Lightweight Data-driven ECG Classification Approach with Explainable CAM Output
This repository contains the implementation of the lightweight CNN-based ECG classification approach with integrated explainable AI (XAI) capabilities presented in the paper **"Lightweight Data-driven ECG Classification Approach with Explainable CAM Output"** at **The Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC)** 2025 by Rytis Augustauskas, Ana Santos Rodrigues, Daivaras Sokas, Otilia Bularca, and Vaidotas Marozas.
### High-level overview
This repository describes data wrangling for the [PTBXL](https://physionet.org/content/ptb-xl/1.0.3/) dataset and binary classification problem, where the data is separated into 2 classes **NORMAL** and **ABNORMAL**, with explainability in single iteration (*approach can be applied in multiclass classification problems*):  
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/demo_xai_size_reduced.gif" width="600"/>

### Data
PTBXL 12 lead ECG is utilized as input for classification:  
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/orig.png" width="600"/>

### Model
Minimalistic 1D convolutional neural network with binary output is utilized (can be scaled in network class):  
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/network_sample.png" width="600"/>

### Pipeline
The following data pipeline is utilized in this investigation. Step:
1. Loading signal to the representable container (NumPy array)
2. Baseline wander removal
3. Apply standard scaling for each lead separately (according to the training dataset)
4. Introduce noise and transformation to make more variety of data (introduced only while training)
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/Pipeline.png" width="200"/>


### XAI
[Class activation map](http://cnnlocalization.csail.mit.edu/Zhou_Learning_Deep_Features_CVPR_2016_paper.pdf) idea is implemented for signal data. Please check the further description to understand the implementation:  
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/CAM_XAI_sample.gif" width="500"/>

## Installation
Execute line in terminal to set environment:<br />
```
pip install -r requirements.txt
```

## Content
PTB-XL data wrangling sample in [**ptbxl_data_loader.ipynb**](https://github.com/rytisss/SignalCNNTransformer/blob/main/ptbxl_data_loader.ipynb)

Change the path to the data to start quickly [**PATH_TO_DATA**](https://github.com/rytisss/SignalCNNTransformer/blob/6bec3985a3f3215f080f2ed2ef33b4643d7cb419/ptbxl_data_classification.ipynb#L62)<br />

https://github.com/rytisss/SignalCNNTransformer/assets/22094617/10178b02-da65-449c-b1b2-daa9cfb842df

The example consists of:
1. Data loading<br />
2. Visualization
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/orig.png" width="600"/>
3. Splitting (train, test, valid according to [*We therefore propose to use folds 1-8 as training set, fold 9 as validation set and fold 10 as test set*](https://physionet.org/content/ptb-xl/1.0.3/) <br />
4. Preprocessing (detrending with 10th degree polynomial)
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/orig_detrend.png" width="600"/>
5. Scaling (Standard according to the training set)<br />
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/scaling.png" width="600"/>
6. Augmentation pipeline
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/augmentation_2.png" width="600"/>
7. Training for classification with automatics learning rate scheduling<br />
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/training_statistics.png" width="600"/>
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/confusion_matrix.png" width="600"/>
8. Prediction<br /> 
9. Explainability with CAM as additional non-trainable output to get explainable results with binary prediction<br />
<img src="https://github.com/rytisss/SignalCNNTransformer/blob/main/res/xai_branch.png" width="300"/>
