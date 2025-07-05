# Lightweight Data-driven ECG Classification Approach with Explainable CAM Output
This repository contains the implementation of the lightweight CNN-based ECG classification approach with integrated explainable AI (XAI) capabilities presented in the paper **"Lightweight Data-driven ECG Classification Approach with Explainable CAM Output"** at **The Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC) 2025** by Rytis Augustauskas, Ana Santos Rodrigues, Daivaras Sokas, Otilia Bularca, and Vaidotas Marozas.
### High-level overview
This repository describes data wrangling for the [PTBXL](https://physionet.org/content/ptb-xl/1.0.3/) dataset and binary classification problem, where the data is separated into 2 classes **NORMAL** and **ABNORMAL**. While the current implementation is designed for binary classification with integrated explainability in a single iteration, the approach is also adaptable to multiclass classification tasks and supports different CNN architectures. The codebase includes the full workflow:
- Data loading and overview
- Dataset splitting and preprocessing (with optional augmentation)
- Model training and evaluation
- Explainability analysis and visualization

<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/demo_xai_size_reduced.gif" width="600"/>

### Integrated explainability idea
This work adapts a class activation map (CAM)-based explainability technique—originally designed for 2D image data—to 1D time-series ECG signals. The method enhances model interpretability by identifying which parts of the input signal most influenced the prediction.
A non-trainable CAM output layer is added after the global average pooling layer. It computes feature importance by taking the dot product of the latent feature maps and the output layer weights. The result is a single explainability heatmap aligned with the input signal, rescaled to match its original length and normalized to the [0, 1] range.
The explainability output is generated post-training and does not affect model parameters. In binary classification, one CAM map is produced. For multiclass problems, separate maps can be created per class. Importantly, this addition increases computational complexity by only ~15% while maintaining the same number of parameters (on the presented architecture).  
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/xai_branch.png" width="300"/>

## Quick start (installation)

Clone repository:<br />
```
git clone https://github.com/rytisss/XAI_SignalCAM.git
cd XAI_SignalCAM
```

Execute the line in the terminal to set up the environment (install 3rdParties):<br />
```
pip install -r requirements.txt
```

Open **Jupyter**:
```
jupyter notebook
```



## Content overview
PTB-XL data wrangling sample in [**ptbxl_data_loader.ipynb**](https://github.com/rytisss/SignalCNNTransformer/blob/main/ptbxl_data_loader.ipynb)
